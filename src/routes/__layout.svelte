<script>
	import Navbar from '$components/Navbar.svelte';
</script>

<Navbar />

<main>
	<slot />
</main>


<style>
    main {
        padding-top: 2rem;
    }
</style>