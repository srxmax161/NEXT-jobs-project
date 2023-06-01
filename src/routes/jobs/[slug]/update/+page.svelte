<script>
    import { PUBLIC_BACKEND_BASE_URL} from '$env/static/public'
    import { goto } from '$app/navigation'
    import { getUserId, getJobId } from '../../../../utils/auth';

    let jobId;
    let formErrors = {}

    function afterUpdateJobs(){
        goto('/')
    }

    async function updateJobs(evt){
        evt.preventDefault() 
        const getLocalData = getUserId();
    
    const inputData = {
			user: getLocalData,
			title: evt.target['title'].value,
			minAnnualCompensation: evt.target['minAnnualCompensation'].value,
			maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
			employer: evt.target['employer'].value,
			location: evt.target['location'].value,
			description: evt.target['description'].value,
			requirements: evt.target['requirements'].value,
			applicationInstructions: evt.target['applicationInstructions'].value
		};

		const resp = await fetch(PUBLIC_BACKEND_BASE_URL + `/api/collections/jobs/records/:${jobId}`, {
			method: 'PATCH',
			mode: 'cors',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify(inputData)
		});

		if (resp.status === 200) {
			afterUpdateJobs();
		} else {
			const res = await resp.json;
			formErrors = res.data;
		}
    }
</script>

<h1 class="text-center text-3xl font-bold display-flex align-middle">POST JOBS</h1>
<div>
	<form on:submit={updateJobs}>
		<div class="form-control w-full left">
			<label class="label" for="job title">
				<span class="label-text">Job Title</span>
			</label>
			<input
				type="text"
				name="title"
				placeholder="Please input your job title"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form=control w=full">
			<label class="label" for="minAnnualCompensation">
				<span class="label-text">Minimum Annual Compensation</span>
			</label>
			<input
				type="text"
				name="minAnnualCompensation"
				placeholder="Please input your minimum annual compensation"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form=control w=full">
			<label class="label" for="maxAnnualCompensation">
				<span class="label-text">Maximum Annual Compensation</span>
			</label>
			<input
				type="text"
				name="maxAnnualCompensation"
				placeholder="Please input your maximum annual compensation"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form=control w=full">
			<label class="label" for="employer">
				<span class="label-text">Company Name</span>
			</label>
			<input
				type="text"
				name="employer"
				placeholder="Please input your company name"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form=control w=full">
			<label class="label" for="location">
				<span class="label-text">Job Location</span>
			</label>
			<input
				type="text"
				name="location"
				placeholder="Please input your job location"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form=control w=full">
			<label class="label" for="description">
				<span class="label-text">Description</span>
			</label>
			<input
				type="text"
				name="description"
				placeholder="Please input your job description"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form=control w=full">
			<label class="label" for="requirements">
				<span class="label-text">Requirements</span>
			</label>
			<input
				type="text"
				name="requirements"
				placeholder="Please input your job requirements"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form=control w=full">
			<label class="label" for="applicationInstructions">
				<span class="label-text">Applicaiton Instructions</span>
			</label>
			<input
				type="text"
				name="applicationInstructions"
				placeholder="Please input your application instructions"
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w-full">
			<button class="btn text 3xl">UPDATE JOB</button>
		</div>
	</form>
</div>
