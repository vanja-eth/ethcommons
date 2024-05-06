<script>
  import { navMenu } from '$lib/info'
  import MoonIcon from 'heroicons-svelte/solid/MoonIcon.svelte'
  import SunIcon from 'heroicons-svelte/solid/SunIcon.svelte'
  import { browser } from '$app/environment'
  import { page } from '$app/stores';
  import MenuIcon from 'heroicons-svelte/solid/MenuIcon.svelte'
  import MenuItems from './MenuItems.svelte'
  import Logo from './Logo.svelte';

  let isDarkMode = browser ? Boolean(document.documentElement.classList.contains('dark')) : true
  let isMenuOpen = false;

  $: currentPage = $page.path;

  function toggleMenu() {
    isMenuOpen = !isMenuOpen; 
  }
  function disableTransitionsTemporarily() {
    document.documentElement.classList.add('[&_*]:!transition-none')
    window.setTimeout(() => {
      document.documentElement.classList.remove('[&_*]:!transition-none')
    }, 0)
  }
  
</script>

<header class="flex items-center justify-between w-full py-4 mx-auto lg:pb-8 gap-16"> 
  <Logo />

  <button class="sm:hidden ml-4" on:click={toggleMenu}>
    <MenuIcon class="h-6 w-6" />
  </button>

  <div class={`fixed transform top-0 left-0 w-48 h-full overflow-auto ease-in-out transition-all duration-300 z-30 ${isMenuOpen ? 'translate-x-0' : '-translate-x-full'} sm:hidden ${isDarkMode ? 'bg-black' : 'bg-white'}`}>
    <ul class="flex flex-col gap-2 text-sm w-full p-4">
      <MenuItems {navMenu} />
    </ul>
  </div>

  <div class="relative flex justify-around gap-2 items-center sm:flex hidden">
    
      <ul class="flex flex-col sm:flex-row gap-2 text-sm w-full sm:w-auto">
        <MenuItems {navMenu} />
      </ul>


    <div class="sm:flex hidden justify-center p-1 relative sm:w-auto sm:-space-x-px overflow-hidden sm:rounded">
    </div>
    
    <style>
      .rotate {
        transition: transform 0.3s;
      }
      .rotate:hover {
        transform: rotate(15deg);
      }
    </style>
    
    <button
    type="button"
    role="switch"
    aria-label="Toggle Dark Mode"
    aria-checked={isDarkMode}
    class="w-5 h-5 sm:h-8 sm:w-8 sm:p-1 transition-colors duration-200"
    on:click={() => {
      isDarkMode = !isDarkMode
      localStorage.setItem('isDarkMode', isDarkMode.toString())
  
      disableTransitionsTemporarily()
  
      if (isDarkMode) {
        document.querySelector('html').classList.add('dark')
      } else {
        document.querySelector('html').classList.remove('dark')
      }
  
      // Close the menu on mobile
      if (window.innerWidth <= 768) {
        isMenuOpen = false;
      }
    }}
  >
    {#if isDarkMode}
      <MoonIcon class="hidden text-zinc-500 dark:block hover:text-yellow-500 transition-colors duration-200 rotate" />
    {:else}
      <SunIcon class="block text-zinc-400 dark:hidden hover:text-orange-500 transition-colors duration-200 rotate" />
    {/if}
  </button>
  </div>
</header>