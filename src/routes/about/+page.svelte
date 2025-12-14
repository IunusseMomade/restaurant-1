<script>
  import { 
    Instagram, 
    Facebook, 
    Twitter, 
    Menu as MenuIcon,
    X,
    Award,
    Flame,
    Wine,
    ChefHat
  } from '@lucide/svelte';
  import person_1 from '$lib/assets/images/about/about-section4-1.jpeg?enhanced';
  import person_2 from '$lib/assets/images/about/about-section4-2.jpeg?enhanced';
  import ambient_1 from '$lib/assets/images/about/about-section2-1.jpeg?enhanced';
  import food_1 from '$lib/assets/images/about/about-section2-2.jpeg?enhanced';
	import HeaderSimple from '$lib/components/HeaderSimple.svelte';
  let isMenuOpen = false;
</script>

<div class="min-h-screen bg-white text-gray-800 font-sans selection:bg-[#C5A059] selection:text-white">
  <HeaderSimple/>
  <!-- --- 1. HEADER (Consistent) --- -->
  <!-- <header class="flex flex-col w-full border-b border-gray-200 sticky top-0 z-50 bg-white/95 backdrop-blur-sm transition-all">
    <div class="container mx-auto px-6 py-4 flex justify-between items-center">
      <div class="flex items-center gap-2">
        <div class="font-serif text-3xl font-bold tracking-wider text-gray-900">ISTANBUL</div>
        <div class="h-8 w-[1px] bg-[#C5A059] mx-2"></div>
        <div class="text-xs uppercase tracking-[0.2em] text-gray-500 leading-tight">
          Authentic<br/>Turkish<br/>Cuisine
        </div>
      </div>

      <div class="hidden md:flex items-center gap-8 text-sm font-medium tracking-wide">
        <a href="#" class="hover:text-[#C5A059] transition-colors">HOME</a>
        <a href="#" class="hover:text-[#C5A059] transition-colors">MENUS</a>
        <a href="#" class="text-[#C5A059] transition-colors">STORY</a>
        <a href="#" class="hover:text-[#C5A059] transition-colors">GALLERY</a>
        
        <button class="bg-[#C5A059] text-white px-6 py-2.5 text-xs font-bold uppercase tracking-widest hover:bg-[#a68545] transition-colors shadow-sm ml-4">
          Book A Table
        </button>
      </div>
      <button class="md:hidden" onclick={() => isMenuOpen = !isMenuOpen}>
        {#if isMenuOpen}
          <X size={24} />
        {:else}
          <MenuIcon size={24} />
        {/if}
      </button>
    </div>
  </header> -->


  <!-- --- 2. HERO SECTION --- -->
  <section class="relative w-full h-[70vh] flex items-center justify-center overflow-hidden">
    <div class="absolute inset-0">
      <video
        autoplay
        muted
        loop
        playsinline
        poster="https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&q=80&w=2000"
        class="w-full h-full object-cover"
      >
        <source src="https://videos.pexels.com/video-files/3196236/3196236-uhd_2560_1440_25fps.mp4" type="video/mp4" />
        Your browser does not support the video tag.
      </video>
      <div class="absolute inset-0 bg-black/60"></div>
    </div>
    
    <div class="relative z-10 text-center text-white px-6 max-w-4xl mx-auto">
      <div class="w-20 h-[1px] bg-[#C5A059] mx-auto mb-8"></div>
      <h1 class="font-serif text-5xl md:text-7xl mb-6 leading-tight tracking-tight">
        A Tale of Two Cities
      </h1>
      <p class="text-gray-200 font-light text-lg md:text-xl tracking-wide leading-relaxed">
        Where the ancient traditions of the Ottoman Empire meet contemporary fine dining.
      </p>
    </div>
  </section>

  <!-- --- 3. THE ORIGIN STORY --- -->
  <section class="py-20 md:py-32 container mx-auto px-6">
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 lg:gap-24 items-center">
      <!-- Text Side -->
      <div class="order-2 lg:order-1">
        <span class="text-[#C5A059] text-xs font-bold uppercase tracking-[0.2em] mb-4 block">Our Heritage</span>
        <h2 class="font-serif text-4xl md:text-5xl text-gray-900 mb-8 leading-tight">
          Bringing the Bosphorus <br/> to Your Table
        </h2>
        <div class="space-y-6 text-gray-500 font-light text-base leading-8">
          <p>
            Founded on the belief that food is a bridge between cultures, Istanbul Restaurant began as a humble dream to recreate the vibrant energy of Turkey's Grand Bazaar and the sophisticated palates of Beyoğlu.
          </p>
          <p>
            Our philosophy is simple yet uncompromising: <strong>Honesty in ingredients, mastery in technique.</strong> We import our spices directly from Gaziantep, our olive oil from the Aegean coast, and our meats are locally sourced but aged according to centuries-old Turkish traditions.
          </p>
          <p>
            Every dish served is a tribute to the <em>Ocakbaşı</em> culture—the fireside gathering where sharing food equates to sharing life.
          </p>
        </div>
        <div class="mt-10">
          <enhanced:img src={person_2}/>
          <!-- <p class="text-xs uppercase tracking-widest text-gray-400 mt-2">Mehmet Yilmaz, Founder</p> -->
        </div>
      </div>

      <!-- Image Side - Collage Effect -->
      <div class="order-1 lg:order-2 relative">
        <div class="relative z-10">
          <enhanced:img 
            src={ambient_1}
            alt="Chef Plating" 
            class="w-full h-auto shadow-2xl"
          />
        </div>
        <!-- Decorative Offset Image -->
        <div class="absolute -bottom-12 -left-12 w-2/3 z-20 hidden md:block">
           <enhanced:img 
             src={food_1}
             alt="Steak Detail" 
             class="w-full h-auto shadow-xl border-8 border-white" 
           />
        </div>
        <!-- Gold Frame Outline -->
        <div class="absolute -top-6 -right-6 w-full h-full border border-[#C5A059] -z-10 hidden md:block"></div>
      </div>
    </div>
  </section>

  <!-- --- 4. PILLARS OF EXCELLENCE (Icons) --- -->
  <section class="bg-[#FAFAFA] py-24 border-t border-gray-100">
    <div class="container mx-auto px-6">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-12 text-center">
        
        <div class="flex flex-col items-center group">
          <div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
            <Flame class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
          </div>
          <h4 class="font-serif text-lg mb-3">Charcoal Fire</h4>
          <p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
            Authentic oak charcoal cooking for distinct smokey flavor.
          </p>
        </div>

        <div class="flex flex-col items-center group">
          <div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
            <Award class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
          </div>
          <h4 class="font-serif text-lg mb-3">Prime Cuts</h4>
          <p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
            Only the finest, high-marble beef makes it to our dry-aging lockers.
          </p>
        </div>

        <div class="flex flex-col items-center group">
          <div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
            <Wine class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
          </div>
          <h4 class="font-serif text-lg mb-3">Curated Pairing</h4>
          <p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
            An extensive cellar featuring the best of Turkish and World wines.
          </p>
        </div>

        <div class="flex flex-col items-center group">
          <div class="w-16 h-16 rounded-full bg-white border border-gray-200 flex items-center justify-center mb-6 shadow-sm group-hover:border-[#C5A059] transition-colors">
            <ChefHat class="text-gray-800 group-hover:text-[#C5A059] transition-colors" size={28} />
          </div>
          <h4 class="font-serif text-lg mb-3">Master Craft</h4>
          <p class="text-xs text-gray-500 uppercase tracking-widest leading-relaxed">
            Led by Chef Ismail, combining 30 years of culinary excellence.
          </p>
        </div>

      </div>
    </div>
  </section>

  <!-- --- 5. THE CHEF'S TABLE (Dark Section) --- -->
  <section class="bg-[#111] text-white py-24 md:py-32 relative overflow-hidden">
    <!-- Background Texture -->
    <div class="absolute top-0 left-0 w-full h-full opacity-10 pointer-events-none">
       <svg width="100%" height="100%">
         <pattern id="pattern-circles" x="0" y="0" width="40" height="40" patternUnits="userSpaceOnUse">
           <circle cx="2" cy="2" r="1" fill="#fff" />
         </pattern>
         <rect x="0" y="0" width="100%" height="100%" fill="url(#pattern-circles)" />
       </svg>
    </div>

    <div class="container mx-auto px-6 relative z-10">
      <div class="flex flex-col md:flex-row items-center gap-16">
         <div class="md:w-1/2">
           <div class="relative">
             <enhanced:img 
               src={person_1}
               alt="Head Chef" 
               class="w-full h-[500px] object-cover "
             />
            
           </div>
         </div>
         
         <div class="md:w-1/2">
            <Award class="text-[#C5A059] mb-6" size={40} />
            <h2 class="font-serif text-4xl md:text-5xl mb-8 leading-tight">
              "Cooking is not just about ingredients, recipes, and cooking. It’s about harnessing imagination, empowerment, and creativity."
            </h2>
            <div class="w-16 h-1 bg-[#C5A059] mb-8"></div>
            <p class="text-gray-400 font-light leading-relaxed mb-8">
              Chef Ismail brings a unique perspective to Istanbul Restaurant. Having trained in both Istanbul's historic kitchens and Paris's Michelin-starred establishments, he creates dishes that respect tradition while embracing modern refinement.
            </p>
            <button class="border border-white text-white px-8 py-3 text-xs font-bold uppercase tracking-widest hover:bg-[#C5A059] hover:border-[#C5A059] transition-all">
              View Menu
            </button>
         </div>
      </div>
    </div>
  </section>

  <!-- --- 6. CTA / ATMOSPHERE --- -->
  <section class="py-24 text-center">
     <div class="container mx-auto px-6">
       <h2 class="font-serif text-4xl text-gray-900 mb-6">Experience the Magic</h2>
       <p class="text-gray-500 font-light max-w-2xl mx-auto mb-10">
         Whether it is a romantic dinner, a family celebration, or a business lunch, we promise an atmosphere as memorable as the meal.
       </p>
       <button class="bg-[#C5A059] text-white px-10 py-4 text-sm font-bold uppercase tracking-[0.15em] hover:bg-[#a68545] transition-all shadow-xl hover:shadow-2xl transform hover:-translate-y-1">
          Reserve Your Table
        </button>
     </div>
  </section>

  <!-- --- 7. FOOTER (Consistent) --- -->
  <footer class="bg-[#0a0a0a] text-white pt-20 pb-8 border-t-[3px] border-[#C5A059]">
    <div class="container mx-auto px-6">
      <div class="flex flex-col md:flex-row justify-between items-start mb-16 gap-10">
         <div class="max-w-sm">
            <div class="font-serif text-2xl tracking-widest mb-6">ISTANBUL</div>
            <h5 class="text-xs font-bold text-gray-400 uppercase tracking-widest mb-4">Join our list</h5>
            <div class="flex border-b border-gray-700 pb-2">
               <input type="email" placeholder="Enter your email address" class="bg-transparent border-none outline-none text-white w-full placeholder-gray-600 text-sm" />
               <button class="text-xs font-bold uppercase text-[#C5A059] tracking-widest">Subscribe</button>
            </div>
         </div>
         <div class="grid grid-cols-2 md:grid-cols-3 gap-x-12 gap-y-8 text-xs text-gray-400 font-light leading-loose">
           <div>
              <h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">Restaurant</h6>
              <ul class="space-y-1">
                <li class="hover:text-[#C5A059] cursor-pointer">About Us</li>
                <li class="hover:text-[#C5A059] cursor-pointer">Private Dining</li>
                <li class="hover:text-[#C5A059] cursor-pointer">Gift Vouchers</li>
              </ul>
           </div>
           <div>
              <h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">Contact</h6>
              <ul class="space-y-1">
                <li class="hover:text-[#C5A059] cursor-pointer">+258 84 123 4567</li>
                <li class="hover:text-[#C5A059] cursor-pointer">info@istanbul.co.mz</li>
                <li class="hover:text-[#C5A059] cursor-pointer">Maputo, Mozambique</li>
              </ul>
           </div>
           <div>
              <h6 class="text-white font-bold uppercase tracking-wider mb-4 text-[10px]">Follow Us</h6>
              <div class="flex gap-4 mt-2">
                <Instagram size={18} class="hover:text-[#C5A059] cursor-pointer" />
                <Facebook size={18} class="hover:text-[#C5A059] cursor-pointer" />
              </div>
           </div>
         </div>
      </div>
      <div class="border-t border-gray-900 pt-8 flex flex-col md:flex-row justify-between items-center gap-6">
        <div class="text-[10px] text-gray-600 uppercase tracking-widest text-center">
          © 2024 Istanbul Restaurant. All Rights Reserved.
        </div>
      </div>
    </div>
  </footer>
</div>
