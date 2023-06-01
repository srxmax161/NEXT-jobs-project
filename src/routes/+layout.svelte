<script>
  import {goto} from '$app/navigation';
  import { loggedIn } from './store.js';
  import '../app.css';

function logOut(evt){
  evt.preventDefault();

  loggedIn.set(false)

  goto('/')
}

// let isLoggedIn;

// loggedIn.subscribe(value => {
//   isLoggedIn = value;
// });
  </script>

<nav class='flex justify-between'>
  <div>
  <button class='btn'>
    <a href='/'>DATABASE</a>
  </button>
  </div>
  <div>
    {#if $loggedIn == false}
      <button class='btn'>
        <a href='/users/new'>SIGNUP</a>
      </button>
      <button class='btn'>
        <a href='/login'>LOG IN</a>
      </button>
    {:else}
      <button class="btn">
        <a href='/jobs/new'>POST JOBS</a>
      </button>
      <button class="btn" on:click={logOut}>LOG OUT
      </button>
    {/if}
  </div>
</nav>



  <slot />
  