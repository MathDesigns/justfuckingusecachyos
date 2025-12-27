<script lang="ts">
	import './layout.css';
	import AuroraBackground from '$lib/AuroraBackground.svelte';
	import favicon from '$lib/assets/favicon.png';

	let { children } = $props();
</script>

<AuroraBackground />

<svelte:head><link rel="icon" href={favicon} /></svelte:head>
<div class="relative z-10">
{@render children()}
</div>
