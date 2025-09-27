<script>
	import '../app.css';
	import '../styles.css';
	import favicon from '$lib/assets/favicon.svg';
	
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=PT+Serif:wght@400;700&display=swap" rel="stylesheet">
	<link rel="icon" href={favicon} />
	<title>Osrs Calculator App</title>
</svelte:head>

<Header />

<main>
	{@render children?.()}
</main>

<Footer />
