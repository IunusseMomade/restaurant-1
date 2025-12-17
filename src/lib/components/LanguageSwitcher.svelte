<script>
	import { page } from '$app/state';
	import { locales, localizeHref } from '$lib/paraglide/runtime';
	import { onMount } from 'svelte';

	const labels = {
		pt: 'Pt',
		en: 'En',
		tr: 'Tr'
	};

	// Helper to determine current language from URL since languageTag() is causing issues
	function getCurrentLocale(pathname) {
		// Check if path starts with any locale (e.g. /en/...) or is exactly the locale (e.g. /en)
		const found = locales.find(l => pathname.startsWith(`/${l}/`) || pathname === `/${l}`);
		// If found, return it. If not, assume default locale (usually 'pt' based on your settings)
		return found || 'pt';
	}

	let currentLocale = $derived(getCurrentLocale(page.url.pathname));
	let isHighlighted = $state(true);

	onMount(() => {
		// Keep highlighted for 3 seconds then fade out
		const timer = setTimeout(() => {
			isHighlighted = false;
		}, 3000);
		return () => clearTimeout(timer);
	});
</script>

<!-- Reduced size, padding, and added opacity for subtlety. Expands opacity on hover. -->
<div class="fixed right-0 top-1/2 -translate-y-1/2 z-50 flex flex-col gap-1 bg-white/90 backdrop-blur-sm p-1 rounded-l-md shadow-md border border-r-0 border-gray-200 transition-opacity duration-1000 {isHighlighted ? 'opacity-100' : 'opacity-40 hover:opacity-100'}">
	{#each locales as locale}
		<a 
			href={localizeHref(page.url.pathname, { locale })}
			class="w-7 h-7 flex items-center justify-center rounded text-[10px] font-bold transition-all duration-200
			{currentLocale === locale 
				? 'bg-[#C5A059] text-white shadow-sm' 
				: 'text-gray-500 hover:bg-gray-100 hover:text-gray-900'}"
			aria-label="Switch to {labels[locale] ?? locale}"
			hreflang={locale}
			data-sveltekit-noscroll
		>
			{labels[locale] ?? locale.toUpperCase()}
		</a>
	{/each}
</div>
