<script>
	export let data;
    import humanize from 'humanize-plus'
</script>
<!--create header with xl font size and bold font at the center of the page-->
<h1 class="text-center text-xl font-bold display-flex align-middle">Find Your Next Job</h1>

<div class="overflow-x-auto w-full">
    {#each data.jobs as job}
    
</div>
