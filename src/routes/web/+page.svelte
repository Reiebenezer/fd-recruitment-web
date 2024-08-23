<script lang="ts">
	import { goto } from '$app/navigation';
	import BgComponent from '$lib/svelte/bg-component.svelte';
	import Logo from '$lib/svelte/logo.svelte';
	import { fly, type FlyParams } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

	function validate() {
		goto('/home', { replaceState: true });
	}

	const flyParams: FlyParams = {
		y: 100,
		duration: 600,
		easing: quintOut,
		delay: 300
	};

	type ChangeEventHandler = Event & { currentTarget: EventTarget & HTMLInputElement };

	function change(e: ChangeEventHandler) {
		localStorage.setItem('control-number', e.currentTarget.value);
	}
</script>

<div class="bg">
	<BgComponent />

	<div class="content" in:fly={flyParams} out:fly={{ ...flyParams, delay: 0 }}>
		<Logo type="blue" />
		<h1>Forum-Dimensions</h1>
		<p>Dear FD hopeful,</p>
		<p><strong>Thank you for heeding the call of the Pido Army.</strong></p>
		<p>
			Now that you're here, it's time to test whether you got what it takes to become one of us.
		</p>
		<p>
			Can you create a website layout? We will have to see. For now, accomplish the form below by
			adding your control number (e.g. FD-01) on the space provided.
		</p>

		<form class="cta" on:submit|preventDefault={validate}>
			<input
				type="text"
				placeholder="Control Number"
				pattern="[Ff][Dd]-\d\d"
				required
				on:change={change}
			/>
			<button>Get Started</button>
		</form>
	</div>
</div>

<style lang="scss">
	.bg {
		position: fixed;
		inset: 15vh 0 0;

		display: grid;
		align-items: center;

		@media screen and (width > 768px) {
			inset: 0 40vw 0 0;
		}
	}

	.content {
		padding: 3rem;

		display: grid;
		gap: 1rem;

		max-width: 60ch;

		@media screen and (width > 768px) {
			padding-right: 6rem;
		}

		p {
			text-wrap: pretty;
		}

		strong {
			color: var(--light-accent);
		}

		button {
			display: block;
			margin-top: 0.5rem;
		}
	}
</style>
