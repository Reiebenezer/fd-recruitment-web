<script lang="ts">
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	onMount(() => goto(localStorage.getItem('control-number') ? '/web/home' : '/web'))
</script>

<slot />