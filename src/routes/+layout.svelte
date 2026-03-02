<script>
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
    import Header from "$lib/components/Header.svelte";
    import Footer from "$lib/components/Footer.svelte";

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<Header/>
<main class="md:max-w-2xl">
    {@render children()}
</main>
<Footer/>