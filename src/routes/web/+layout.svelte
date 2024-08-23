<script lang="ts">
	import '@fontsource/calistoga';
	import '@fontsource/rubik/400.css';
	import '@fontsource/rubik/600.css';
	import '@phosphor-icons/web/bold';
	import '$lib/scss/defaults.scss';

	import logo from '$lib/assets/logo.svg';
	import bg from '$lib/assets/bg.jpg';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	let loaded = false;

	function load(image: HTMLImageElement) {
		if (image.complete) loaded = true;
		else image.onload = () => (loaded = true);
	}
</script>

<svelte:head>
	<link rel="icon" href={logo} />
	<title>FD Recruitment | Web Assets</title>
</svelte:head>

<main class:loaded>
	<img src={bg} alt="" use:load loading="lazy" />
	{#if loaded}
		<slot />
	{/if}
</main>

<style lang="scss">
	main {
		display: grid;
		height: 100svh;

		img {
			position: fixed;

			left: 50%;
			bottom: 0;

			height: 130%;

			transform: translateX(-40%);
			z-index: -1;

			opacity: 0;
			transition: opacity 300ms ease-out;
		}

		&.loaded img {
			opacity: 1;
		}
	}
</style>
