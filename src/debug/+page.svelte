<script>
    import { goto } from '$app/navigation';
    import { authenticateUser } from '../../utils/auth';
    
    let isLoggedIn = false;
    
    async function handleSubmit(evt){
            evt.preventDefault()
    
        const userData = {
            username: evt.target['username'].value,
            password: evt.target['password'].value
    }
        
        const res = await authenticateUser(userData.username, userData.password);
    
        if(res.success){
            isLoggedIn = true;
            goto('jobs/new');
        
        }
        else {
            console.error('Please sign up as user');
        }
    
    
        function login(username, password){
        isLoggedIn = true;  
        }
    
        function logout(){
        isLoggedIn =false ; 
        }
    }
    </script>
    
    <form on:submit={handleSubmit} class="w-1/3"></form>
        <div class="form-control w-full">
            <label class="label" for="username">
             <span class="label-text">Username</span>
         </label>
        <input type="username"  name="username" placeholder="" class="input input-bordered w-full" required />
    </div>
    
    <div class="form-control w-full">
        <label class="label" for="password">
            <span class="label-text">Password</span>
        </label>
        <input type="password"  name="password" placeholder="" class="input input-bordered w-full" required />
    </div>
    
    <div class="form-control w-full mt-4">
        <button class="btn btn-md">Log IN</button>
    </div>