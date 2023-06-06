<script>
    export let data;
    import { PUBLIC_BACKEND_BASE_URL} from '$env/static/public'
    import { goto } from '$app/navigation'
    import { getUserId, getTokenFromLocalStorage } from '../../../../utils/auth';

    let clicked = false
    let formErrors = {}

    function afterUpdateJobs(){
        goto(`/jobs/${data.job.id}`)
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


		const resp = await fetch(PUBLIC_BACKEND_BASE_URL + `/api/collections/jobs/records/${data.job.id}`, {
			method: 'PATCH',
			mode: 'cors',
			headers: {
				'Content-Type': 'application/json',
                'Authorization': getTokenFromLocalStorage()
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
		<div class="form-control w-full left px-36 mt-5">
			<label class="label" for="job title">
				<span class="label-text">Job Title</span>
			</label>
			<input
				type="text"
				name="title"
				bind:value={data.job.title}
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w=full px-36 mt-5">
			<label class="label" for="minAnnualCompensation">
				<span class="label-text">Minimum Annual Compensation</span>
			</label>
			<input
				type="text"
				name="minAnnualCompensation"
				bind:value={data.job.minAnnualCompensation}
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w=full px-36 mt-5">
			<label class="label" for="maxAnnualCompensation">
				<span class="label-text">Maximum Annual Compensation</span>
			</label>
			<input
				type="text"
				name="maxAnnualCompensation"
				bind:value={data.job.maxAnnualCompensation}
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w=full px-36 mt-5">
			<label class="label" for="employer">
				<span class="label-text">Company Name</span>
			</label>
			<input
				type="text"
				name="employer"
				bind:value={data.job.employer}
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w=full px-36 mt-5">
			<label class="label" for="location">
				<span class="label-text">Job Location</span>
			</label>
			<input
				type="text"
				name="location"
				bind:value={data.job.location}
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w=full px-36 mt-5">
			<label class="label" for="description">
				<span class="label-text">Description</span>
			</label>
			<textarea
				type="text"
				name="description"
				bind:value={data.job.description}
				class="textarea textarea-bordered w-full h-56"
				required
			/>
		</div>
		<div class="form-control w=full px-36 mt-5">
			<label class="label" for="requirements">
				<span class="label-text">Requirements</span>
			</label>
			<input
				type="text"
				name="requirements"
				bind:value={data.job.requirements}
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w=full px-36 mt-5">
			<label class="label" for="applicationInstructions">
				<span class="label-text">Application Instructions</span>
			</label>
			<input
				type="text"
				name="applicationInstructions"
				bind:value={data.job.applicationInstructions}
				class="input input-bordered w-full"
				required
			/>
		</div>
		<div class="form-control w-full px-36 mt-5">
            {#if clicked}
            <button class="btn btn-md bg-purple-700 hover:bg-purple-800 loading">Update Job</button>
        {:else}
            <button class="btn btn-md bg-purple-700 hover:bg-purple-800">Update Job</button>
        {/if}
		</div>
	</form>
</div>
