<script>
  import { fade, fly } from 'svelte/transition';
  import { cubicOut } from 'svelte/easing';

  let isDrawerOpen = false;
  
  function toggleDrawer() {
    isDrawerOpen = !isDrawerOpen;
  }
</script>

<nav class="bg-white shadow-sm">
  <div class="container mx-auto px-4">
    <div class="flex justify-between items-center h-16">
      <div class="flex items-center">
        <span class="text-2xl font-bold text-green-600">Deodar Labs</span>
      </div>
      
      <!-- Desktop Menu -->
      <div class="hidden md:flex space-x-8">
        <a href="#services" class="text-gray-600 hover:text-green-600 transition">Services</a>
        <a href="#about" class="text-gray-600 hover:text-green-600 transition">About</a>
        <a href="#contact" class="text-gray-600 hover:text-green-600 transition">Contact</a>
      </div>

      <!-- Mobile Menu Button -->
      <button class="md:hidden" on:click={toggleDrawer}>
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
        </svg>
      </button>
    </div>
  </div>
</nav>

<!-- Mobile Drawer -->
{#if isDrawerOpen}
  <div class="fixed inset-0 z-50 md:hidden" transition:fade={{ duration: 300 }}>
    <!-- Backdrop -->
    <div class="fixed inset-0 bg-black bg-opacity-50" on:click={toggleDrawer}></div>
    
    <!-- Drawer -->
    <div class="fixed right-0 top-0 w-64 h-full bg-gradient-to-b from-green-50 to-white shadow-lg"
         transition:fly={{ x: 300, duration: 300, easing: cubicOut }}>
      
      <div class="p-6">
        <button class="mb-6 text-green-600 hover:text-green-700 transition" on:click={toggleDrawer}>
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
          </svg>
        </button>
        
        <div class="flex flex-col space-y-6">
          {#each ['Services', 'About', 'Contact'] as item, index}
            <a href="#{item.toLowerCase()}" 
               class="text-lg text-gray-700 hover:text-green-600 transition transform hover:translate-x-2" 
               on:click={toggleDrawer}
               transition:fly={{ y: 20, duration: 200, delay: 100 * index }}>
              {item}
            </a>
          {/each}
        </div>
      </div>
    </div>
  </div>
{/if}