<script lang="ts">
	import { quintOut } from 'svelte/easing';
	import { fade, fly } from 'svelte/transition';

	export let show = false;

	function clickOutside(node: HTMLElement) {
		node.addEventListener('click', (e) => {
			if ((e.target as HTMLElement).closest('.content-window') === null) {
				show = false;
			}
		});
	}
</script>

{#if show}
	<div class="dialog" transition:fade use:clickOutside>
		<div class="content-window" transition:fly={{ y: 100, duration: 600, easing: quintOut }}>
			<button class="close" on:click={() => (show = false)}><i class="ph-bold ph-x"></i></button>
			<slot />
		</div>
	</div>
{/if}

<style lang="scss">
	.dialog {
		position: fixed;
		inset: 0;

        z-index: 1;

		padding-inline: 10vw;
		padding-block: 10vh;

		backdrop-filter: blur(10px) brightness(0.6);
		-webkit-backdrop-filter: blur(10px) brightness(0.6);

        display: grid;
        place-items: center;
        justify-content: center;

		.close {
			font-size: 1rem;
			align-self: flex-end;

            width: fit-content;
		}

		.content-window {
			display: flex;
            flex-direction: column;

			background-color: var(--light-shade);
			border-radius: 1rem;
            
			overflow: hidden;

			max-height: 100%;
            max-width: 100%;

			padding: 2rem;
		}
	}
</style>
