<script>
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
    import Header from "$lib/components/Header.svelte";
    import AppBar from "$lib/components/AppBar.svelte";

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<AppBar />
<Header/>
<main>
    {@render children()}
</main>
