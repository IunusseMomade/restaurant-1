<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.png';
	import LanguageSwitcher from '$lib/components/LanguageSwitcher.svelte';
	import { page } from '$app/state';

	let { children } = $props();
	export const prerender = true;
</script>

<svelte:head>
	<link rel="icon" type="image/png" href={favicon} />
</svelte:head>

<LanguageSwitcher />

{#key page.url.pathname}
	{@render children()}
{/key}
