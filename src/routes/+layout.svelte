<script>
  import { loggedIn } from './store.js';
  import './app.css';

function logOut(evt){
  evt.preventDefault();

  loggedIn.set(false)

  goto('/')
}

let isLoggedIn;

loggedIn.subscribe(value => {
  isLoggedIn = value;
});
  </script>

<nav class='flex justify-between'>
  <div>
  <button class='btn'>
    <a href='/'>DATABASE</a>
  </button>
  </div>
  <div>
    {#if !isLoggedIn}
      <button class='btn'>
        <a href='/users/new'>SIGNUP</a>
      </button>
      <button class='btn'>
        <a href='/login'>LOG IN</a>
      </button>
    {:else}
      <button class="btn">
        <a href='/postjobs'>POST JOBS</a>
      </button>
      <button class="btn" form on:submit={logOut}>
        <a href='/'>LOG OUT</a>
      </button>
    {/if}
  </div>
</nav>



  <slot />
  