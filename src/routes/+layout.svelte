<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import LanguageSwitcher from '$lib/components/LanguageSwitcher.svelte';
	import { page } from '$app/state';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<LanguageSwitcher />

{#key page.url.pathname}
	{@render children()}
{/key}
