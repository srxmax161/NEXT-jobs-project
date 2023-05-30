<script>
    import { PUBLIC_BACKEND_BASE_URL} from '$env/static/public';
    export let data;
    import {goto} from '$app/navigation'
    let formErrors ={};

    function afterPostjobs(){
        goto('/')
    }
    async function inputform(evt){
        evt.preventDefault();

        const inputData = {
            job_title: evt.target['job title'].value,
            min_compensation: evt.target['min compensation'].value,
            max_compensation: evt.target['max compensation'].value,
            company_name: evt.target['company name'].value,
            job_location: evt.target['job location'].value,
            description: evt.target['description'].value,
            requirements: evt.target['requirements'].value,
            application_instructions: evt.target['application instructions'].value
        }

        const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/users/records',{
            method:'POST',
            mode: 'cors',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(inputData)
        });

        if (resp.status == 200) {
            const res = await inputform(inputData.job_title, inputData.min_compensation, inputData.max_compensation, inputData.company_name, inputData.job_location, inputData.description, inputData.requirements, inputData.application_instructions);

            if (res.success) {
                afterPostjobs();
            } else {
                throw 'Please try again'
            }
        } else {
            const res = await resp.json;
            formErrors = res.data
        }
    }
</script>


<h1 class='text-center text-3xl font-bold display-flex align-middle'>POST JOBS</h1>
<div>
    <form on:submit={inputform}>
        <div class='form-control w-full left'>
            <label class="label" for="job title">
                <span class='label-text'>Job Title</span>
            </label>
            <input 
                type="text" 
                name="job title" 
                placeholder="Please input your job title" 
                class="input input-bordered w-full" 
                required
                />
        </div>
        <div class="form=control w=full">
            <label class="label" for="min compensation">
                <span class ="label-text">Minimum Annual Compensation</span>
            </label>
            <input type="text"
                   name="minimum annual compensation"
                   placeholder="Please input your minimum annual compensation"
                   class="input input-bordered w-full"
                   required
                   />
        </div>
         <div class="form=control w=full">
            <label class="label" for="min compensation">
                <span class ="label-text">Maximum Annual Compensation</span>
            </label>
            <input type="text"
                   name="maximum annual compensation"
                   placeholder="Please input your maximum annual compensation"
                   class="input input-bordered w-full"
                   required
                   />
        </div>
        <div class="form=control w=full">
            <label class="label" for="company name">
                <span class ="label-text">Company Name</span>
            </label>
            <input type="text"
                   name="company name"
                   placeholder="Please input your company name"
                   class="input input-bordered w-full"
                   required
                   />
        </div>
        <div class="form=control w=full">
            <label class="label" for="job location">
                <span class ="label-text">Job Location</span>
            </label>
            <input type="text"
                   name="Job Location"
                   placeholder="Please input your job location"
                   class="input input-bordered w-full"
                   required
                   />
        </div>
        <div class="form=control w=full">
            <label class="label" for="description">
                <span class ="label-text">Description</span>
            </label>
            <input type="text"
                   name="Description"
                   placeholder="Please input your job description"
                   class="input input-bordered w-full"
                   required
                   />
        </div>
        <div class="form=control w=full">
            <label class="label" for="requirements">
                <span class ="label-text">Requirements</span>
            </label>
            <input type="text"
                   name="requiremnts"
                   placeholder="Please input your job requirements"
                   class="input input-bordered w-full"
                   required
                   />
        </div>
        <div class="form=control w=full">
            <label class="label" for="application instructions">
                <span class ="label-text">Applicaiton Instructions</span>
            </label>
            <input type="text"
                   name="application instructions"
                   placeholder="Please input your application instructions"
                   class="input input-bordered w-full"
                   required
                   />
        </div>
        <div class="form-control w-full">
            <button class="btn text 3xl">POST JOB</button>
    </form>
</div>
