<script>
	import { goto } from '$app/navigation';
	import { loggedIn } from './store.js';
	import '../app.css';
	import Themes from '../components/themes.svelte';

	function logOut(evt) {
		evt.preventDefault();

		loggedIn.set(false);

		goto('/');
	}
  

	// let isLoggedIn;

	// loggedIn.subscribe(value => {
	//   isLoggedIn = value;
	// });
</script>

<nav class="flex justify-between mt-5 px-3">
	<div>
		<button class="btn">
			<a href="/">DATABASE</a>
		</button>
	</div>
  <Themes/>
    <div>
		{#if $loggedIn == false}
    <div>
    </div>
			<button class="btn">
				<a href="/users/new">SIGNUP</a>
			</button>
			<button class="btn">
				<a href="/login">LOG IN</a>
			</button>
		{:else}
			<button class="btn">
				<a href="/jobs/new">POST JOBS</a>
			</button>
			<button class="btn" on:click={logOut}>LOG OUT </button>
		{/if}
	</div>
</nav>

<slot />
