<script lang="ts">
	import { quintOut } from "svelte/easing";
	import { fly, type FlyParams } from "svelte/transition";

    const flyV: FlyParams = {
        y: 250,
        duration: 600,
        easing: quintOut,
    }

    const flyH: FlyParams = {
        ...flyV,
        y: 0,
        x: -250
    }
</script>

<div class="h" transition:fly|global>
	<span in:fly={{ ...flyH, delay: 0   }} out:fly={{ ...flyH, delay: 200 }}></span>
	<span in:fly={{ ...flyH, delay: 100 }} out:fly={{ ...flyH, delay: 100 }}></span>
	<span in:fly={{ ...flyH, delay: 200 }} out:fly={{ ...flyH, delay: 0   }}></span>
</div>

<div class="v">
	<span in:fly={{ ...flyV, delay: 0   }} out:fly={{ ...flyV, delay: 200 }}></span>
	<span in:fly={{ ...flyV, delay: 100 }} out:fly={{ ...flyV, delay: 100 }}></span>
	<span in:fly={{ ...flyV, delay: 200 }} out:fly={{ ...flyV, delay: 0   }}></span>
</div>

<style lang="scss">
	div,
	span {
		position: absolute;
		inset: 0;

		z-index: -1;
	}

    span {
        box-shadow: 4px -4px var(--shadow);
    }

	.v {
		transform: skewY(5deg);
	}

	.h {
		transform: skewX(5deg);
		display: none;
	}

	span:nth-child(1) {
		background-color: var(--dark-accent);
	}

	span:nth-child(2) {
		background-color: var(--light-accent);
		translate: 0 1.5rem;
	}

	span:nth-child(3) {
		background-color: var(--light-shade);
		translate: 0 3rem;
	}

	@media screen and (width > 768px) {
		.v {
			display: none;
		}
		.h {
			display: unset;
		}

		span:nth-child(2) {
			translate: -1.5rem 0;
		}
		span:nth-child(3) {
			translate: -3rem 0;
		}
	}
</style>
