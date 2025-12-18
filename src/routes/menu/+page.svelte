<script>
	import HeaderSimple from '$lib/components/HeaderSimple.svelte';
	import ImageViewer from '$lib/components/ImageViewer.svelte';
	import * as m from '$lib/paraglide/messages';
	import { onMount } from 'svelte';
	import {
		Clock,
		MapPin,
		Phone,
		ChevronRight,
		Instagram,
		Facebook,
		Twitter,
		Mail,
		Menu as MenuIcon,
		X,
		Share2,
		Search,
		ChevronDown
	} from '@lucide/svelte';

	let isMenuOpen = $state(false);
	let activeCategory = $state('starters');
	let viewerImages = $state(null);
	let viewerStartIndex = $state(0);
	let isUserClicking = $state(false); // Prevent observer from overriding manual clicks
	/** @type {HTMLDivElement | null} */
	let categoryNavScroller = null;

	/** @param {WheelEvent} e */
	function onCategoryNavWheel(e) {
		if (!categoryNavScroller) return;
		// Treat vertical wheel as horizontal scroll for the category nav.
		if (Math.abs(e.deltaY) > Math.abs(e.deltaX)) {
			categoryNavScroller.scrollLeft += e.deltaY;
		}
	}

	/** @param {any} item */
	function imagesFromMenuItem(item) {
		const images = Array.isArray(item?.images) ? item.images.filter(Boolean) : [];
		if (images.length) return images;
		return item?.image ? [item.image] : [];
	}

	/** @param {string} categoryId */
	function menuItemsFor(categoryId) {
		return (/** @type {any} */ (menuItems))?.[categoryId] ?? [];
	}

	/** @param {string} categoryId */
	function imagesForCategory(categoryId) {
		return menuItemsFor(categoryId).flatMap(imagesFromMenuItem);
	}

	/** @param {string} categoryId @param {any} item */
	function openMenuImageViewer(categoryId, item) {
		const all = imagesForCategory(categoryId);
		const clicked = imagesFromMenuItem(item)[0];
		const nextImages = all.length ? all : clicked ? [clicked] : [];
		viewerImages = nextImages;
		viewerStartIndex = clicked ? Math.max(0, nextImages.indexOf(clicked)) : 0;
	}

	// --- Menu Data Structure ---
	let menuCategories = $derived([
		{ id: 'starters', label: m.cat_starters() },
		{ id: 'breakfast', label: m.cat_breakfast() },
		{ id: 'soups', label: m.cat_soups() },
		{ id: 'salads', label: m.cat_salads() },
		{ id: 'toast', label: m.cat_toast() },
		{ id: 'burgers', label: m.cat_burgers() },
		{ id: 'doner', label: m.cat_doner() },
		{ id: 'chicken', label: m.cat_chicken() },
		{ id: 'kebab', label: m.cat_kebab() },
		{ id: 'special', label: m.cat_special() },
		{ id: 'steakhouse', label: m.cat_steakhouse() },
		{ id: 'pasta', label: m.cat_pasta() },
		{ id: 'pide', label: m.cat_pide() },
		{ id: 'pizza', label: m.cat_pizza() },
		{ id: 'sushi', label: m.cat_sushi() },
		{ id: 'seafood', label: m.cat_seafood() },
		{ id: 'vegetable', label: m.cat_vegetable() },
		{ id: 'kids', label: m.cat_kids() },
		{ id: 'drinks', label: m.cat_drinks() }
	]);

	//menu imports
	import baklava from '$lib/assets/images/menu/baklava-1.jpeg?enhanced';

	// Helper to get items. In a real app, you might fetch this or have a huge object.
	// I've mapped a few items per category to demonstrate.
	let menuItems = $derived({
		starters: [
			{ name: m.item_icli_kofte(), desc: m.desc_icli_kofte(), price: "400", image: "https://images.unsplash.com/photo-1603083563476-660951622619?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_hummus(), desc: m.desc_hummus(), price: "400", dietary: "V", image: "https://images.unsplash.com/photo-1637949385162-e416fb15b2ce?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_avci_boregi(), desc: m.desc_avci_boregi(), price: "500", image: "https://images.unsplash.com/photo-1601050690597-df0568f70950?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_rice_mix(), desc: m.desc_rice_mix(), price: "250" },
			{ name: m.item_potato_portion(), desc: m.desc_potato_portion(), price: "250", image: "https://images.unsplash.com/photo-1630384060421-cb20d0e0649d?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_shrimp_tartlets(), desc: m.desc_shrimp_tartlets(), price: "160" },
			{ name: m.item_garlic_bread(), desc: m.desc_garlic_bread(), price: "350", image: "https://images.unsplash.com/photo-1619535860434-ba1d8fa12536?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_bread_feta(), desc: m.desc_bread_feta(), price: "400" },
			{ name: m.item_samosas(), desc: m.desc_samosas(), price: "160", image: "https://images.unsplash.com/photo-1601050690597-df0568f70950?auto=format&fit=crop&q=80&w=400" }
		],
		breakfast: [
			{ name: m.item_complete_breakfast(), desc: m.desc_complete_breakfast(), price: "2200", image: "https://images.unsplash.com/photo-1533089862017-5614ec87e284?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_menemen(), desc: m.desc_menemen(), price: "550", image: "https://images.unsplash.com/photo-1626132647523-66f5bf380027?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_kavurmali_yumurta(), desc: m.desc_kavurmali_yumurta(), price: "550" },
			{ name: m.item_plain_omelette(), desc: m.desc_plain_omelette(), price: "600", image: "https://images.unsplash.com/photo-1510693206972-df098062cb71?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_mini_breakfast(), desc: m.desc_mini_breakfast(), price: "900" },
			{ name: m.item_crepe_plate(), desc: m.desc_crepe_plate(), price: "600", image: "https://images.unsplash.com/photo-1519676867240-f03562e64548?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_stuffed_croissant(), desc: m.desc_stuffed_croissant(), price: "220", image: "https://images.unsplash.com/photo-1555507036-ab1f4038808a?auto=format&fit=crop&q=80&w=400" }
		],
		soups: [
			{ name: m.item_lentil_soup(), desc: m.desc_lentil_soup(), price: "350", dietary: "V", image: "https://images.unsplash.com/photo-1547592166-23acbe346499?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_lamb_soup(), desc: m.desc_lamb_soup(), price: "1000" },
			{ name: m.item_vegetable_soup(), desc: m.desc_vegetable_soup(), price: "450", image: "https://images.unsplash.com/photo-1547592166-23acbe346499?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_fish_soup(), desc: m.desc_fish_soup(), price: "550" },
			{ name: m.item_tripe_soup(), desc: m.desc_tripe_soup(), price: "550" },
			{ name: m.item_head_soup(), desc: m.desc_head_soup(), price: "600" },
			{ name: m.item_bisque_soup(), desc: m.desc_bisque_soup(), price: "600", image: "https://images.unsplash.com/photo-1548943487-a2e4e43b485c?auto=format&fit=crop&q=80&w=400" }
		],
		salads: [
			{ name: m.item_tuna_salad(), desc: m.desc_tuna_salad(), price: "700", image: "https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_salmon_salad(), desc: m.desc_salmon_salad(), price: "900", image: "https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_mediterranean_salad(), desc: m.desc_mediterranean_salad(), price: "650", image: "https://images.unsplash.com/photo-1540189549336-e6e99c3679fe?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_shepherd_salad(), desc: m.desc_shepherd_salad(), price: "400" },
			{ name: m.item_chicken_salad(), desc: m.desc_chicken_salad(), price: "700", image: "https://images.unsplash.com/photo-1550304943-4f24f54ddde9?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_walnut_salad(), desc: m.desc_walnut_salad(), price: "650" },
			{ name: m.item_cacik(), desc: m.desc_cacik(), price: "400", image: "https://images.unsplash.com/photo-1577859714523-5f0b6c98ece7?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_yogurt_1kg(), desc: m.desc_yogurt_1kg(), price: "300" },
			{ name: m.item_yogurt_6kg(), desc: m.desc_yogurt_6kg(), price: "1600" }
		],
		toast: [
			{ name: m.item_prego_bread(), desc: m.desc_prego_bread(), price: "650", image: "https://images.unsplash.com/photo-1604467715878-83e57e8bc129?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_toast(), desc: m.desc_toast(), price: "200", image: "https://images.unsplash.com/photo-1584776293029-440f8f279542?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_tombik_sandwich(), desc: m.desc_tombik_sandwich(), price: "550" },
			{ name: m.item_cheese_toast(), desc: m.desc_cheese_toast(), price: "400" },
			{ name: m.item_ham_toast(), desc: m.desc_ham_toast(), price: "500" },
			{ name: m.item_mix_toast(), desc: m.desc_mix_toast(), price: "650" },
			{ name: m.item_chicken_toast(), desc: m.desc_chicken_toast(), price: "600" },
			{ name: m.item_tuna_toast(), desc: m.desc_tuna_toast(), price: "600" }
		],
		burgers: [
			{ name: m.item_classic_burger(), desc: m.desc_classic_burger(), price: "650", image: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_istanbul_special(), desc: m.desc_istanbul_special(), price: "800", image: "https://images.unsplash.com/photo-1594212699903-ec8a3eca50f5?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_zinger(), desc: m.desc_zinger(), price: "800", image: "https://images.unsplash.com/photo-1615297348954-4b85f59c95f4?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_cuban_onion(), desc: m.desc_cuban_onion(), price: "800" },
			{ name: m.item_uzivizi_burger(), desc: m.desc_uzivizi_burger(), price: "550" }
		],
		doner: [
			{ name: m.item_iskender_kebab(), desc: m.desc_iskender_kebab(), price: "1150", image: "https://images.unsplash.com/photo-1652622959664-037415347d76?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_durum_doner(), desc: m.desc_durum_doner(), price: "550", image: "https://images.unsplash.com/photo-1676300185297-0365d6345558?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_tombik_doner(), desc: m.desc_tombik_doner(), price: "650" },
			{ name: m.item_porsiyon_doner(), desc: m.desc_porsiyon_doner(), price: "1000", image: "https://images.unsplash.com/photo-1529042410759-befb1204b468?auto=format&fit=crop&q=80&w=400" }
		],
		chicken: [
			{ name: m.item_half_chicken(), desc: m.desc_half_chicken(), price: "500", image: "https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_whole_chicken(), desc: m.desc_whole_chicken(), price: "900", image: "https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_chicken_doner_plate(), desc: m.desc_chicken_doner_plate(), price: "850" },
			{ name: m.item_chicken_shawarma(), desc: m.desc_chicken_shawarma(), price: "550", image: "https://images.unsplash.com/photo-1676300185297-0365d6345558?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_chicken_breast(), desc: m.desc_chicken_breast(), price: "700", image: "https://images.unsplash.com/photo-1632778149955-e80f8ceca2e8?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_schnitzel(), desc: m.desc_schnitzel(), price: "800", image: "https://images.unsplash.com/photo-1599921841143-819065a55cc6?auto=format&fit=crop&q=80&w=400" }
		],
		kebab: [
			{ name: m.item_adana_spicy(), desc: m.desc_adana_spicy(), price: "900", image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_pistachio_kebab(), desc: m.desc_pistachio_kebab(), price: "1200" },
			{ name: m.item_urfa_nonspicy(), desc: m.desc_urfa_nonspicy(), price: "900" },
			{ name: m.item_adana_wrap(), desc: m.desc_adana_wrap(), price: "550" },
			{ name: m.item_urfa_wrap(), desc: m.desc_urfa_wrap(), price: "550" },
			{ name: m.item_grilled_wings(), desc: m.desc_grilled_wings(), price: "1000", image: "https://images.unsplash.com/photo-1567620832903-9fc6debc209f?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_chicken_kebab(), desc: m.desc_chicken_kebab(), price: "800", image: "https://images.unsplash.com/photo-1603360946369-dc9bb6f54262?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_lamb_skewered(), desc: m.desc_lamb_skewered(), price: "1050", image: "https://images.unsplash.com/photo-1603360946369-dc9bb6f54262?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_cop_sis(), desc: m.desc_cop_sis(), price: "1050" },
			{ name: m.item_cop_sis_durum(), desc: m.desc_cop_sis_durum(), price: "700" },
			{ name: m.item_mix_kebab_1(), desc: m.desc_mix_kebab_1(), price: "1500", image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_mix_kebab_2(), desc: m.desc_mix_kebab_2(), price: "2700" },
			{ name: m.item_mix_kebab_4(), desc: m.desc_mix_kebab_4(), price: "5000" },
			{ name: m.item_mix_kebab_6(), desc: m.desc_mix_kebab_6(), price: "7200" },
			{ name: m.item_grilled_meatballs(), desc: m.desc_grilled_meatballs(), price: "950", image: "https://images.unsplash.com/photo-1529042410759-befb1204b468?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_kasarli_kofte(), desc: m.desc_kasarli_kofte(), price: "1200" },
			{ name: m.item_chicken_cop_sis(), desc: m.desc_chicken_cop_sis(), price: "1200" },
			{ name: m.item_adana_cop_sis(), desc: m.desc_adana_cop_sis(), price: "1200" },
			{ name: m.item_ali_nazik(), desc: m.desc_ali_nazik(), price: "1200" }
		],
		special: [
			{ name: m.item_patlicanli_kebap(), desc: m.desc_patlicanli_kebap(), price: "1200", image: "https://images.unsplash.com/photo-1603083563476-660951622619?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_domatesli_kebap(), desc: m.desc_domatesli_kebap(), price: "1200" },
			{ name: m.item_beyti_sarma(), desc: m.desc_beyti_sarma(), price: "1500", image: "https://images.unsplash.com/photo-1644364935906-74995a43c493?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_kusbasi_guvec(), desc: m.desc_kusbasi_guvec(), price: "1300", image: "https://images.unsplash.com/photo-1534939561126-855b8675edd7?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_kebap_soltani(), desc: m.desc_kebap_soltani(), price: "1100" },
			{ name: m.item_filet_sultani(), desc: m.desc_filet_sultani(), price: "1000" },
			{ name: m.item_sac_kavurma_1(), desc: m.desc_sac_kavurma_1(), price: "1200", image: "https://images.unsplash.com/photo-1606851094655-b2593a9af63f?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_sac_kavurma_2(), desc: m.desc_sac_kavurma_2(), price: "2000" },
			{ name: m.item_prego_plate(), desc: m.desc_prego_plate(), price: "1100" },
			{ name: m.item_kusleme(), desc: m.desc_kusleme(), price: "1750" },
			{ name: m.item_fes_kebab(), desc: m.desc_fes_kebab(), price: "2100" },
			{ name: m.item_black_pepper_steak(), desc: m.desc_black_pepper_steak(), price: "1700" },
			{ name: m.item_hunkar_begendi(), desc: m.desc_hunkar_begendi(), price: "1800" },
			{ name: m.item_roasted_steak(), desc: m.desc_roasted_steak(), price: "1700" },
			{ name: m.item_fajita_beef(), desc: m.desc_fajita_beef(), price: "1400", image: "https://images.unsplash.com/photo-1534790566855-4cb788d389ec?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_fajita_chicken(), desc: m.desc_fajita_chicken(), price: "1200" },
			{ name: m.item_fajita_shrimp(), desc: m.desc_fajita_shrimp(), price: "1500" },
			{ name: m.item_steak_mushrooms(), desc: m.desc_steak_mushrooms(), price: "1700" },
			{ name: m.item_istanbul_sarma(), desc: m.desc_istanbul_sarma(), price: "2000" },
			{ name: m.item_picanha(), desc: m.desc_picanha(), price: "1550", image: "https://images.unsplash.com/photo-1594041680534-e8c8cdebd659?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_picanha_brazilian(), desc: m.desc_picanha_brazilian(), price: "1850" }
		],
		steakhouse: [
			{ name: m.item_istanbul_steak(), desc: m.desc_istanbul_steak(), price: "1800", image: "https://images.unsplash.com/photo-1600891964092-4316c288032e?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_veal_steak(), desc: m.desc_veal_steak(), price: "1600", image: "https://images.unsplash.com/photo-1600891964092-4316c288032e?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_tbone(), desc: m.desc_tbone(), price: "1650", image: "https://images.unsplash.com/photo-1546833998-877b37c2e5b4?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_dallas_steak(), desc: m.desc_dallas_steak(), price: "1700" },
			{ name: m.item_lokum_delight(), desc: m.desc_lokum_delight(), price: "1900", image: "https://images.unsplash.com/photo-1558030006-450675393462?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_striploin(), desc: m.desc_striploin(), price: "1600" },
			{ name: m.item_tomahawk(), desc: m.desc_tomahawk(), price: "2200", image: "https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_ny_strip(), desc: m.desc_ny_strip(), price: "1800" },
			{ name: m.item_lamb_rice(), desc: m.desc_lamb_rice(), price: "1750" },
			{ name: m.item_lamb_steak(), desc: m.desc_lamb_steak(), price: "1900" },
			{ name: m.item_loin(), desc: m.desc_loin(), price: "1700" },
			{ name: m.item_lamb_curry(), desc: m.desc_lamb_curry(), price: "1600" },
			{ name: m.item_lamb_chops(), desc: m.desc_lamb_chops(), price: "1800", image: "https://images.unsplash.com/photo-1606625007229-25d80a346e3e?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_lamb_ribs(), desc: m.desc_lamb_ribs(), price: "1600" },
			{ name: m.item_lamb_skewer_steak(), desc: m.desc_lamb_skewer_steak(), price: "1600" }
		],
		pasta: [
			{ name: m.item_penne_arrabiata(), desc: m.desc_penne_arrabiata(), price: "800", image: "https://images.unsplash.com/photo-1608835291093-394b0c943a75?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_spaghetti_carbonara(), desc: m.desc_spaghetti_carbonara(), price: "850", image: "https://images.unsplash.com/photo-1612874742237-6526221588e3?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_linguine_di_mare(), desc: m.desc_linguine_di_mare(), price: "900", image: "https://images.unsplash.com/photo-1563379926898-05f4575a45d8?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_fettuccine_alfredo(), desc: m.desc_fettuccine_alfredo(), price: "900", image: "https://images.unsplash.com/photo-1645112411341-6c4fd023714a?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_spaghetti_basilico(), desc: m.desc_spaghetti_basilico(), price: "800" }
		],
		pide: [
			{ name: m.item_mixed_pide(), desc: m.desc_mixed_pide(), price: "1200", image: "https://images.unsplash.com/photo-1626700051175-6818013e1d4f?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_chicken_pide(), desc: m.desc_chicken_pide(), price: "1000" },
			{ name: m.item_beef_cheese_pide(), desc: m.desc_beef_cheese_pide(), price: "1100" },
			{ name: m.item_lahmacun(), desc: m.desc_lahmacun(), price: "500", image: "https://images.unsplash.com/photo-1626700051175-6818013e1d4f?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_grilled_beef_pide(), desc: m.desc_grilled_beef_pide(), price: "1100" },
			{ name: m.item_cheese_pide(), desc: m.desc_cheese_pide(), price: "850" },
			{ name: m.item_sausage_cheese_pide(), desc: m.desc_sausage_cheese_pide(), price: "1100" },
			{ name: m.item_minced_meat_pide(), desc: m.desc_minced_meat_pide(), price: "1000" },
			{ name: m.item_pide_small(), desc: m.desc_pide_small(), price: "700" }
		],
		pizza: [
			{ name: m.item_pizza_chicken_s(), desc: m.desc_pizza_chicken_s(), price: "800", image: "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_pizza_chicken_m(), desc: m.desc_pizza_chicken_m(), price: "1200" },
			{ name: m.item_pizza_mexicana_s(), desc: m.desc_pizza_mexicana_s(), price: "800" },
			{ name: m.item_pizza_mexicana_m(), desc: m.desc_pizza_mexicana_m(), price: "1200" },
			{ name: m.item_pizza_margarita_s(), desc: m.desc_pizza_margarita_s(), price: "600", image: "https://images.unsplash.com/photo-1574071318508-1cdbab80d002?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_pizza_margarita_m(), desc: m.desc_pizza_margarita_m(), price: "1000" },
			{ name: m.item_pizza_tuna_s(), desc: m.desc_pizza_tuna_s(), price: "800" },
			{ name: m.item_pizza_tuna_m(), desc: m.desc_pizza_tuna_m(), price: "1200" },
			{ name: m.item_pizza_family(), desc: m.desc_pizza_family(), price: "1600" },
			{ name: m.item_pizza_shrimp_s(), desc: m.desc_pizza_shrimp_s(), price: "750" },
			{ name: m.item_pizza_shrimp_m(), desc: m.desc_pizza_shrimp_m(), price: "1150" },
			{ name: m.item_pizza_regina_s(), desc: m.desc_pizza_regina_s(), price: "750" },
			{ name: m.item_pizza_regina_m(), desc: m.desc_pizza_regina_m(), price: "1150" },
			{ name: m.item_pizza_mix_s(), desc: m.desc_pizza_mix_s(), price: "850" },
			{ name: m.item_pizza_mix_m(), desc: m.desc_pizza_mix_m(), price: "1250" },
			{ name: m.item_pizza_turkish_s(), desc: m.desc_pizza_turkish_s(), price: "800" },
			{ name: m.item_pizza_turkish_m(), desc: m.desc_pizza_turkish_m(), price: "1200" }
		],
		sushi: [
			{ name: m.item_maki_salmon(), desc: m.desc_maki_salmon(), price: "500", image: "https://images.unsplash.com/photo-1579871494447-9811cf80d66c?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_maki_tuna(), desc: m.desc_maki_tuna(), price: "450" },
			{ name: m.item_maki_shrimp(), desc: m.desc_maki_shrimp(), price: "420" },
			{ name: m.item_maki_veg(), desc: m.desc_maki_veg(), price: "400" },
			{ name: m.item_maki_mix(), desc: m.desc_maki_mix(), price: "600" },
			{ name: m.item_temaki_salmon(), desc: m.desc_temaki_salmon(), price: "410" },
			{ name: m.item_temaki_tuna(), desc: m.desc_temaki_tuna(), price: "390" },
			{ name: m.item_temaki_shrimp(), desc: m.desc_temaki_shrimp(), price: "390" },
			{ name: m.item_temaki_veg(), desc: m.desc_temaki_veg(), price: "340" },
			{ name: m.item_sashimi_salmon(), desc: m.desc_sashimi_salmon(), price: "500", image: "https://images.unsplash.com/photo-1534482421-64566f976cfa?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_sashimi_tuna(), desc: m.desc_sashimi_tuna(), price: "450" },
			{ name: m.item_uramaki_salmon(), desc: m.desc_uramaki_salmon(), price: "500" },
			{ name: m.item_uramaki_tuna(), desc: m.desc_uramaki_tuna(), price: "450" },
			{ name: m.item_uramaki_shrimp(), desc: m.desc_uramaki_shrimp(), price: "420" },
			{ name: m.item_uramaki_veg(), desc: m.desc_uramaki_veg(), price: "400" },
			{ name: m.item_tempura_shrimp(), desc: m.desc_tempura_shrimp(), price: "420" },
			{ name: m.item_tempura_squid(), desc: m.desc_tempura_squid(), price: "420" },
			{ name: m.item_seared_salmon(), desc: m.desc_seared_salmon(), price: "450" },
			{ name: m.item_seared_shrimp(), desc: m.desc_seared_shrimp(), price: "420" },
			{ name: m.item_seared_tuna(), desc: m.desc_seared_tuna(), price: "420" },
			{ name: m.item_roses_salmon(), desc: m.desc_roses_salmon(), price: "450" },
			{ name: m.item_roses_shrimp(), desc: m.desc_roses_shrimp(), price: "420" },
			{ name: m.item_roses_tuna(), desc: m.desc_roses_tuna(), price: "420" },
			{ name: m.item_spicy_roses_salmon(), desc: m.desc_spicy_roses_salmon(), price: "450" },
			{ name: m.item_spicy_roses_shrimp(), desc: m.desc_spicy_roses_shrimp(), price: "420" },
			{ name: m.item_spicy_roses_tuna(), desc: m.desc_spicy_roses_tuna(), price: "420" },
			{ name: m.item_philadelphia_sushi(), desc: m.desc_philadelphia_sushi(), price: "840", image: "https://images.unsplash.com/photo-1611143669185-af224c5e3252?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_sandwiches_salmon(), desc: m.desc_sandwiches_salmon(), price: "450" },
			{ name: m.item_sandwiches_tuna(), desc: m.desc_sandwiches_tuna(), price: "420" },
			{ name: m.item_sandwiches_shrimp(), desc: m.desc_sandwiches_shrimp(), price: "420" },
			{ name: m.item_turkish_sushi_kebab(), desc: m.desc_turkish_sushi_kebab(), price: "350" },
			{ name: m.item_turkish_sushi_shawarma(), desc: m.desc_turkish_sushi_shawarma(), price: "350" }
		],
		seafood: [
			{ name: m.item_grilled_grouper(), desc: m.desc_grilled_grouper(), price: "1800", image: "https://images.unsplash.com/photo-1519708227418-c8fd9a32b7a2?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_grilled_shrimp(), desc: m.desc_grilled_shrimp(), price: "1800", image: "https://images.unsplash.com/photo-1565680018434-b513d5e5fd47?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_grilled_red_fish(), desc: m.desc_grilled_red_fish(), price: "1600" },
			{ name: m.item_seafood_family(), desc: m.desc_seafood_family(), price: "5000" },
			{ name: m.item_grilled_squid(), desc: m.desc_grilled_squid(), price: "1700", image: "https://images.unsplash.com/photo-1599084993091-1cb5c0721cc6?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_fish_fillet(), desc: m.desc_fish_fillet(), price: "1800" },
			{ name: m.item_cataplana_1(), desc: m.desc_cataplana_1(), price: "1800" },
			{ name: m.item_cataplana_2(), desc: m.desc_cataplana_2(), price: "2800" },
			{ name: m.item_scaled_grouper(), desc: m.desc_scaled_grouper(), price: "1800" }
		],
		vegetable: [
			{ name: m.item_veg_lasagna(), desc: m.desc_veg_lasagna(), price: "800", image: "https://images.unsplash.com/photo-1574837695388-9265d08508db?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_sauteed_veg(), desc: m.desc_sauteed_veg(), price: "600" },
			{ name: m.item_veg_toast(), desc: m.desc_veg_toast(), price: "500" },
			{ name: m.item_pasta_mushroom(), desc: m.desc_pasta_mushroom(), price: "800" },
			{ name: m.item_veg_flat_bread(), desc: m.desc_veg_flat_bread(), price: "1000" },
			{ name: m.item_veg_pizza_s(), desc: m.desc_veg_pizza_s(), price: "750" },
			{ name: m.item_veg_pizza_m(), desc: m.desc_veg_pizza_m(), price: "1150" }
		],
		kids: [
			{ name: m.item_kids_meatballs(), desc: m.desc_kids_meatballs(), price: "500", image: "https://images.unsplash.com/photo-1529042410759-befb1204b468?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_kids_sausage(), desc: m.desc_kids_sausage(), price: "500" },
			{ name: m.item_kids_pasta(), desc: m.desc_kids_pasta(), price: "550", image: "https://images.unsplash.com/photo-1598866594230-a7c12756260f?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_kids_burger(), desc: m.desc_kids_burger(), price: "550" },
			{ name: m.item_kids_nugget(), desc: m.desc_kids_nugget(), price: "500", image: "https://images.unsplash.com/photo-1562967914-608f82629710?auto=format&fit=crop&q=80&w=400" }
		],
		drinks: [
			{ name: m.item_water_l(), desc: m.desc_water_l(), price: "150" },
			{ name: m.item_water_s(), desc: m.desc_water_s(), price: "80" },
			{ name: m.item_ayran(), desc: m.desc_ayran(), price: "150", image: "https://images.unsplash.com/photo-1626132647523-66f5bf380027?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_lemonade(), desc: m.desc_lemonade(), price: "200", image: "https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_coca_cola(), desc: m.desc_coca_cola(), price: "100" },
			{ name: m.item_coca_zero(), desc: m.desc_coca_zero(), price: "100" },
			{ name: m.item_sprite(), desc: m.desc_sprite(), price: "100" },
			{ name: m.item_sparkling_water(), desc: m.desc_sparkling_water(), price: "150" },
			{ name: m.item_soda(), desc: m.desc_soda(), price: "100" },
			{ name: m.item_tonic(), desc: m.desc_tonic(), price: "100" },
			{ name: m.item_ginger_ale(), desc: m.desc_ginger_ale(), price: "100" },
			{ name: m.item_dry_lemon(), desc: m.desc_dry_lemon(), price: "100" },
			{ name: m.item_fanta_orange(), desc: m.desc_fanta_orange(), price: "100" },
			{ name: m.item_fanta_pineapple(), desc: m.desc_fanta_pineapple(), price: "100" },
			{ name: m.item_fanta_grape(), desc: m.desc_fanta_grape(), price: "100" },
			{ name: m.item_twist(), desc: m.desc_twist(), price: "100" },
			{ name: m.item_sparletta_strawberry(), desc: m.desc_sparletta_strawberry(), price: "100" },
			{ name: m.item_sparletta_cream_soda(), desc: m.desc_sparletta_cream_soda(), price: "100" },
			{ name: m.item_cappy_orange(), desc: m.desc_cappy_orange(), price: "100" },
			{ name: m.item_cappy_exotic(), desc: m.desc_cappy_exotic(), price: "100" },
			{ name: m.item_red_bull(), desc: m.desc_red_bull(), price: "200" },
			{ name: m.item_appletiser_apple(), desc: m.desc_appletiser_apple(), price: "150" },
			{ name: m.item_appletiser_grape(), desc: m.desc_appletiser_grape(), price: "150" },
			{ name: m.item_fruttree(), desc: m.desc_fruttree(), price: "120" },
			{ name: m.item_compal_1l(), desc: m.desc_compal_1l(), price: "200" },
			{ name: m.item_compal_500(), desc: m.desc_compal_500(), price: "100" },
			{ name: m.item_compal_250(), desc: m.desc_compal_250(), price: "70" },
			{ name: m.item_santal_1l(), desc: m.desc_santal_1l(), price: "200" },
			{ name: m.item_santal_250(), desc: m.desc_santal_250(), price: "70" },
			{ name: m.item_ceres_1l(), desc: m.desc_ceres_1l(), price: "200" },
			{ name: m.item_ceres_250(), desc: m.desc_ceres_250(), price: "70" },
			{ name: m.item_espresso(), desc: m.desc_espresso(), price: "100", image: "https://images.unsplash.com/photo-1510707577719-ae7c14805e3a?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_coffee_milk(), desc: m.desc_coffee_milk(), price: "200" },
			{ name: m.item_double_coffee(), desc: m.desc_double_coffee(), price: "150" },
			{ name: m.item_turkish_coffee(), desc: m.desc_turkish_coffee(), price: "150", image: "https://images.unsplash.com/photo-1561047029-3000c68339ca?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_american_coffee(), desc: m.desc_american_coffee(), price: "200" },
			{ name: m.item_decaf(), desc: m.desc_decaf(), price: "150" },
			{ name: m.item_decaf_milk(), desc: m.desc_decaf_milk(), price: "220" },
			{ name: m.item_cappuccino(), desc: m.desc_cappuccino(), price: "200", image: "https://images.unsplash.com/photo-1572442388796-11668a67e53d?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_latte(), desc: m.desc_latte(), price: "200" },
			{ name: m.item_iced_coffee(), desc: m.desc_iced_coffee(), price: "300", image: "https://images.unsplash.com/photo-1517701604599-bb29b5dd7359?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_milk(), desc: m.desc_milk(), price: "120" },
			{ name: m.item_galao(), desc: m.desc_galao(), price: "200" },
			{ name: m.item_hot_chocolate(), desc: m.desc_hot_chocolate(), price: "250", image: "https://images.unsplash.com/photo-1542990253-0d0f5be5f0ed?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_natural_tea(), desc: m.desc_natural_tea(), price: "250" },
			{ name: m.item_cup_tea(), desc: m.desc_cup_tea(), price: "50" },
			{ name: m.item_istanbul_tea(), desc: m.desc_istanbul_tea(), price: "150", image: "https://images.unsplash.com/photo-1597481499750-3e6b22637e12?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_tea_milk(), desc: m.desc_tea_milk(), price: "180" },
			{ name: m.item_indian_tea(), desc: m.desc_indian_tea(), price: "250" },
			{ name: m.item_decaf_espresso_milk(), desc: m.desc_decaf_espresso_milk(), price: "170" },
			{ name: m.item_juice_natural(), desc: m.desc_juice_natural(), price: "350", image: "https://images.unsplash.com/photo-1613478223719-2ab802602423?auto=format&fit=crop&q=80&w=400" },
			{ name: m.item_juice_mix(), desc: m.desc_juice_mix(), price: "400" },
			{ name: m.item_juice_guava(), desc: m.desc_juice_guava(), price: "400" },
			{ name: m.item_juice_mango(), desc: m.desc_juice_mango(), price: "400" },
			{ name: m.item_juice_titama(), desc: m.desc_juice_titama(), price: "400" },
			{ name: m.item_juice_tropical(), desc: m.desc_juice_tropical(), price: "400" },
			{ name: m.item_juice_cordelia(), desc: m.desc_juice_cordelia(), price: "400" }
		]
	});

	const scrollToSection = (id) => {
		activeCategory = id;
		isUserClicking = true;
		const element = document.getElementById(id);
		if (element) {
			const y = element.getBoundingClientRect().top + window.scrollY - 80;
			window.scrollTo({ top: y, behavior: 'smooth' });
		}
		// Reset flag after scroll completes
		setTimeout(() => {
			isUserClicking = false;
		}, 1000);
	};

	onMount(() => {
		const observer = new IntersectionObserver((entries) => {
			// Only update if user isn't manually clicking
			if (!isUserClicking) {
				entries.forEach(entry => {
					if (entry.isIntersecting) {
						activeCategory = entry.target.id;
						const navItem = document.getElementById(`nav-${entry.target.id}`);
						if (navItem) {
							navItem.scrollIntoView({ behavior: 'smooth', block: 'nearest', inline: 'center' });
						}
					}
				});
			}
		}, {
			rootMargin: '-20% 0px -60% 0px',
			threshold: 0
		});

		menuCategories.forEach(cat => {
			const el = document.getElementById(cat.id);
			if (el) observer.observe(el);
		});

		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<link href="https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700&family=Playfair+Display:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
</svelte:head>

<div class="min-h-screen bg-white text-gray-800 font-sans selection:bg-[#C5A059] selection:text-white">
	
	<!-- --- 1. HEADER (Consistent) --- -->
	 <HeaderSimple/>

	<!-- --- 2. HERO SECTION --- -->
	<section class="relative w-full h-[60vh] flex items-center justify-center overflow-hidden">
		<div class="absolute inset-0">
			<img 
				src="https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&q=80&w=2000" 
				alt="Steak grilling" 
				class="w-full h-full object-cover"
			/>
			<div class="absolute inset-0 bg-black/50"></div>
		</div>
		<div class="relative z-10 text-center text-white p-6 animate-fade-in-up">
			<span class="text-[#C5A059] text-xs font-bold uppercase tracking-[0.3em] mb-4 block">{m.hero_subtitle()}</span>
			<h1 class="font-serif text-5xl md:text-7xl mb-6">{m.hero_title()}</h1>
			<p class="max-w-xl mx-auto text-gray-200 font-light text-sm md:text-base leading-relaxed">
				{m.hero_desc()}
			</p>
		</div>
	</section>
<div class="sticky top-0 z-40 bg-white border-b border-gray-100 transition-all duration-300">
    <div
        class="w-full overflow-x-auto scrollbar-hide"
        bind:this={categoryNavScroller}
        onwheel={onCategoryNavWheel}
    >
        <div class="flex flex-nowrap w-max px-6 py-3 gap-6">
            {#each menuCategories as category}
                <button
                    id="nav-{category.id}"
                    type="button"
                    onclick={() => scrollToSection(category.id)}
                    class="shrink-0 whitespace-nowrap px-0 py-2 text-xs font-medium tracking-wider uppercase transition-all duration-200 relative border-b-2
                    {activeCategory === category.id
                        ? 'border-[#C5A059] text-[#C5A059]'
                        : 'border-transparent text-gray-400 hover:text-gray-700'}"
                >
                    {category.label}
                </button>
            {/each}
        </div>
    </div>
</div>

	<!-- --- 3. MENU CONTENT --- -->
	<div class="container mx-auto px-6 py-20 max-w-5xl">
		
		{#each menuCategories as category}
			{#if menuItems[category.id] && menuItems[category.id].length > 0}
				
				<!-- Special Layout for Steakhouse (Dark Theme) -->
				{#if category.id === 'steakhouse'}
					<div id={category.id} class="bg-[#1a1a1a] text-white p-10 md:p-16 -mx-6 md:-mx-20 mb-24 relative overflow-hidden scroll-mt-32 rounded-lg shadow-2xl">
						<!-- Background Texture Effect -->
						<div class="absolute top-0 right-0 w-64 h-64 bg-[#C5A059] rounded-full filter blur-[100px] opacity-10"></div>
						
						<div class="relative z-10">
							<div class="text-center mb-12">
								<span class="text-[#C5A059] tracking-[0.2em] text-xs font-bold uppercase mb-2 block">{m.premium_cuts()}</span>
								<h2 class="font-serif text-4xl uppercase tracking-wide text-white">{category.label}</h2>
							</div>

							<div class="grid grid-cols-1 md:grid-cols-2 gap-x-16 gap-y-12">
								{#each menuItems[category.id] as item}
									<div class="group flex gap-4 items-start">
										{#if item.image}
											<button 
												type="button"
												onclick={() => openMenuImageViewer(category.id, item)} 
												class="shrink-0 bg-transparent border-none p-0 cursor-pointer" 
												aria-label="View full image"
											>
												<img src={item.image} alt={item.name} class="w-20 h-20 object-cover rounded-sm shadow-lg border border-gray-700 hover:opacity-80 transition-opacity" />
											</button>
										{/if}
										<div class="flex-1">
											<div class="flex justify-between items-baseline mb-2 border-b border-gray-700 pb-2">
												<h3 class="font-serif text-xl font-medium text-[#C5A059] group-hover:text-white transition-colors">
													{item.name}
												</h3>
												<span class="font-serif text-xl font-light">{item.price}</span>
											</div>
											<p class="text-gray-400 text-sm font-light leading-relaxed">{item.desc}</p>
										</div>
									</div>
								{/each}
							</div>
						</div>
					</div>

				<!-- Standard Layout for other categories -->
				{:else}
					<div id={category.id} class="mb-24 scroll-mt-32">
						<div class="text-center mb-12">
							{#if category.id === 'starters'}
								<span class="text-[#C5A059] text-4xl block mb-2">~</span>
							{:else}
								<div class="w-16 h-[1px] bg-[#C5A059] mx-auto mb-6"></div>
							{/if}
							<h2 class="font-serif text-4xl text-gray-900 uppercase tracking-wide">{category.label}</h2>
						</div>
						
						<div class="grid grid-cols-1 md:grid-cols-2 gap-x-16 gap-y-10">
							{#each menuItems[category.id] as item}
								<div class="group flex gap-4 items-start">
									{#if item.image}
										<button 
											type="button"
												onclick={() => openMenuImageViewer(category.id, item)} 
											class="shrink-0 bg-transparent border-none p-0 cursor-pointer" 
											aria-label="View full image"
										>
											<img src={item.image} alt={item.name} class="w-20 h-20 object-cover rounded-sm shadow-md hover:opacity-80 transition-opacity" />
										</button>
									{/if}
									<div class="flex-1">
										<div class="flex justify-between items-baseline mb-2 border-b border-dotted border-gray-300 pb-1">
											<h3 class="font-serif text-lg text-gray-800 font-medium group-hover:text-[#C5A059] transition-colors">
												{item.name}
											</h3>
											<span class="font-serif text-lg font-bold text-[#C5A059]">{item.price}</span>
										</div>
										<p class="text-gray-500 text-sm font-light leading-relaxed">{item.desc}</p>
										{#if item.dietary}
											<span class="text-[10px] text-gray-400 uppercase tracking-wider mt-1 block">{item.dietary === 'V' ? m.dietary_veg() : item.dietary}</span>
										{/if}
									</div>
								</div>
							{/each}
						</div>
					</div>

					<!-- Feature Image Break after Starters -->
					{#if category.id === 'starters'}
						<div class="w-full h-[400px] mb-24 relative rounded-sm overflow-hidden">
							<img 
								src="https://images.unsplash.com/photo-1594041680534-e8c8cdebd659?auto=format&fit=crop&q=80&w=1600" 
								alt="Platter"
								class="w-full h-full object-cover"
							/>
							<div class="absolute bottom-0 left-0 bg-white p-8 max-w-sm">
								<h4 class="font-serif text-2xl mb-2">{m.platter_title()}</h4>
								<p class="text-sm text-gray-500 mb-4">{m.platter_desc()}</p>
								<span class="text-[#C5A059] text-xs font-bold uppercase tracking-widest cursor-pointer hover:text-black">{m.view_details()}</span>
							</div>
						</div>
					{/if}
				{/if}
			{/if}
		{/each}

	</div>

	<!-- --- FOOTER (Same as Layout) --- -->
	<footer class="bg-[#0a0a0a] text-white pt-20 pb-8 border-t-[3px] border-[#C5A059]">
		<div class="container mx-auto px-6">
			<div class="flex flex-col md:flex-row justify-between items-start mb-16 gap-10">
				<div class="max-w-sm">
					<div class="font-serif text-2xl tracking-widest mb-6">ISTANBUL</div>
					<h5 class="text-xs font-bold text-gray-400 uppercase tracking-widest mb-4">{m.join_list()}</h5>
					<div class="flex border-b border-gray-700 pb-2">
						<input type="email" placeholder={m.subscribe_placeholder()} class="bg-transparent border-none outline-none text-white w-full placeholder-gray-600 text-sm" />
						<button class="text-xs font-bold uppercase text-[#C5A059] tracking-widest">{m.subscribe_btn()}</button>
					</div>
				</div>
				<div class="grid grid-cols-2 md:grid-cols-3 gap-x-12 gap-y-8 text-xs text-gray-400 font-light leading-loose">
					<div>
						<h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">{m.footer_restaurant()}</h6>
						<ul class="space-y-1">
							<li class="hover:text-[#C5A059] cursor-pointer">{m.footer_about()}</li>
							<li class="hover:text-[#C5A059] cursor-pointer">{m.footer_private()}</li>
							<li class="hover:text-[#C5A059] cursor-pointer">{m.footer_gift()}</li>
						</ul>
					</div>
					<div>
						<h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">{m.footer_contact()}</h6>
						<ul class="space-y-1">
							<li class="hover:text-[#C5A059] cursor-pointer">+258 84 123 4567</li>
							<li class="hover:text-[#C5A059] cursor-pointer">info@istanbul.co.mz</li>
							<li class="hover:text-[#C5A059] cursor-pointer">Maputo, Mozambique</li>
						</ul>
					</div>
					<div>
						<h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">{m.footer_follow()}</h6>
						<div class="flex gap-4 mt-2">
							<Instagram size={18} class="hover:text-[#C5A059] cursor-pointer" />
							<Facebook size={18} class="hover:text-[#C5A059] cursor-pointer" />
						</div>
					</div>
				</div>
			</div>
			<div class="border-t border-gray-900 pt-8 flex flex-col md:flex-row justify-between items-center gap-6">
				<div class="text-[10px] text-gray-600 uppercase tracking-widest text-center">
					{m.footer_rights()}
				</div>
			</div>
		</div>
	</footer>
</div>

<!-- --- IMAGE MODAL (Moved outside main div) --- -->
{#if viewerImages}
	<ImageViewer images={viewerImages} initialIndex={viewerStartIndex} onClose={() => (viewerImages = null)} />
{/if}

<style>
	.font-serif { font-family: 'Playfair Display', serif; }
	.font-sans { font-family: 'Lato', sans-serif; }
	
	.scrollbar-hide::-webkit-scrollbar {
		display: none;
	}
	.scrollbar-hide {
		-ms-overflow-style: none;
		scrollbar-width: none;
	}

	@keyframes fadeInUp {
		from {
			opacity: 0;
			transform: translate3d(0, 40px, 0);
		}
		to {
			opacity: 1;
			transform: translate3d(0, 0, 0);
		}
	}

	.animate-fade-in-up {
		animation: fadeInUp 0.8s ease-out forwards;
	}
</style>
