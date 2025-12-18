<script>
	import Footer from '$lib/components/Footer.svelte';
	import Gallery from '$lib/components/Gallery.svelte';
	import Header from '$lib/components/Header.svelte';
	import Hero from '$lib/components/Hero.svelte';
	import PromoBanner from '$lib/components/PromoBanner.svelte';
	import RelatedVenues from '$lib/components/RelatedVenues.svelte';
	import InfoBar from '$lib/components/InfoBar.svelte';
	import { page } from '$app/state';
	import { localizeHref } from '$lib/paraglide/runtime';
	import * as m from '$lib/paraglide/messages';

	const seoTitle = m.home_seo_title();
	const seoDescription = m.home_seo_description();

	const canonical = $derived(() => `${$page.url.origin}${$page.url.pathname}`.replace(/\/$/, ''));

	const jsonLd = $derived(() =>
		JSON.stringify(
			{
				'@context': 'https://schema.org',
				'@type': 'Restaurant',
				name: 'Istanbul Restaurant',
				url: `${$page.url.origin}${$page.url.pathname}`.replace(/\/$/, ''),
				areaServed: { '@type': 'City', name: 'Maputo' },
				address: { '@type': 'PostalAddress', addressLocality: 'Maputo', addressCountry: 'MZ' },
				servesCuisine: ['Turkish', 'Mediterranean'],
				priceRange: '$$',
				hasMenu: `${$page.url.origin}${localizeHref('/menu')}`,
				openingHoursSpecification: [
					{
						'@type': 'OpeningHoursSpecification',
						dayOfWeek: [
							'Monday',
							'Tuesday',
							'Wednesday',
							'Thursday',
							'Friday',
							'Saturday',
							'Sunday'
						],
						opens: '07:00',
						closes: '23:00'
					}
				],
				hasPOS: [
					{
						'@type': 'FoodEstablishment',
						name: 'Istanbul Restaurant — Maputo Shopping Center',
						address: {
							'@type': 'PostalAddress',
							streetAddress: 'Maputo Shopping Center',
							addressLocality: 'Maputo',
							addressCountry: 'MZ'
						}
					},
					{
						'@type': 'FoodEstablishment',
						name: 'Istanbul Restaurant — Baía-Mall',
						address: {
							'@type': 'PostalAddress',
							streetAddress: 'Baía-Mall',
							addressLocality: 'Maputo',
							addressCountry: 'MZ'
						}
					}
				]
			},
			null,
			0
		)
	);
</script>

<svelte:head>
	<title>{seoTitle}</title>
	<meta name="description" content={seoDescription} />
	<meta name="robots" content="index,follow,max-image-preview:large" />
	<link rel="canonical" href={canonical} />

	<meta property="og:type" content="website" />
	<meta property="og:title" content={seoTitle} />
	<meta property="og:description" content={seoDescription} />
	<meta property="og:url" content={canonical} />
	<meta property="og:site_name" content="Istanbul Restaurant" />
	<meta property="og:locale" content="pt_MZ" />

	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:title" content={seoTitle} />
	<meta name="twitter:description" content={seoDescription} />

	<script type="application/ld+json">{jsonLd}</script>
</svelte:head>

<!-- <Design_1/> -->
 
<Header/>
<Hero/>


<InfoBar/>
<Gallery/>
<RelatedVenues/>
<PromoBanner/>

<Footer/>