<script>
  import * as m from '$lib/paraglide/messages';
  import { Mail, Phone, MapPin } from '@lucide/svelte';
</script>

<section class="py-12 bg-gradient-to-b from-white to-gray-50">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-left">
      <h2 class="mt-2 text-3xl leading-8 font-extrabold tracking-tight text-gray-900 sm:text-4xl 
                 bg-clip-text text-transparent bg-gradient-to-r from-blue-600 to-blue-800">
        {m.contact_us()}
      </h2>
      <p class="mt-4 max-w-2xl text-xl text-gray-500">
        {m.contact_ready()}
      </p>
    </div>
    <div class="mt-12 grid grid-cols-1 md:grid-cols-3 gap-8">
      <!-- Email Section -->
      <div class="flex flex-col items-start p-6 rounded-lg hover:bg-white hover:shadow-lg transition-all duration-300 group">
        <div class="p-3 bg-blue-50 rounded-lg group-hover:scale-110 transition-transform duration-300">
          <Mail class="h-8 w-8 text-blue-600" />
        </div>
        <h3 class="mt-4 text-lg leading-6 font-medium text-gray-900 group-hover:text-blue-600 transition-colors">
          {m.email_title()}
        </h3>
        <p class="mt-2 text-base text-gray-500">
          {m.email_description()}
        </p>
        <a href="mailto:info@ataconstrucoes.com" 
           class="mt-2 text-blue-600 hover:text-blue-800 transition-colors relative after:absolute after:bottom-0 after:left-0 after:w-0 after:h-0.5 after:bg-blue-600 hover:after:w-full after:transition-all">
          info@ataconstrucoes.com
        </a>
      </div>

      <!-- Phone Section -->
      <div class="flex flex-col items-start p-6 rounded-lg hover:bg-white hover:shadow-lg transition-all duration-300 group">
        <div class="p-3 bg-blue-50 rounded-lg group-hover:scale-110 transition-transform duration-300">
          <Phone class="h-8 w-8 text-blue-600" />
        </div>
        <h3 class="mt-4 text-lg leading-6 font-medium text-gray-900 group-hover:text-blue-600 transition-colors">
          {m.phone_title()}
        </h3>
        <p class="mt-2 text-base text-gray-500">
          {m.phone_description()}
        </p>
        <a href="tel:+258843272930" 
           class="mt-2 text-blue-600 hover:text-blue-800 transition-colors relative after:absolute after:bottom-0 after:left-0 after:w-0 after:h-0.5 after:bg-blue-600 hover:after:w-full after:transition-all">
          +258843272930
        </a>
      </div>

      <!-- Office Section -->
      <div class="flex flex-col items-start p-6 rounded-lg hover:bg-white hover:shadow-lg transition-all duration-300 group">
        <div class="p-3 bg-blue-50 rounded-lg group-hover:scale-110 transition-transform duration-300">
          <MapPin class="h-8 w-8 text-blue-600" />
        </div>
        <h3 class="mt-4 text-lg leading-6 font-medium text-gray-900 group-hover:text-blue-600 transition-colors">
          {m.office_title()}
        </h3>
        <p class="mt-2 text-base text-gray-500">
          {m.office_description()}
        </p>
        <p class="mt-2 text-gray-900 font-medium">142 Av. da Malhangalene,<br/>Maputo 1102</p>
      </div>
    </div>
  </div>
</section>