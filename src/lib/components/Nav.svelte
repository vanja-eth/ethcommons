<script>
  import { navMenu } from '$lib/info'
  import MoonIcon from 'heroicons-svelte/solid/MoonIcon.svelte'
  import SunIcon from 'heroicons-svelte/solid/SunIcon.svelte'
  import { browser } from '$app/environment'
  import { page } from '$app/stores';
  import MenuIcon from 'heroicons-svelte/solid/MenuIcon.svelte'
  import MenuItems from './MenuItems.svelte'
  import Logo from './Logo.svelte';

  let menuOpen = false;

  function toggleMenu() {
    menuOpen = !menuOpen;
  }
  
  let isDarkMode = browser ? Boolean(document.documentElement.classList.contains('dark')) : true
  
  $: currentPage = $page.path;

  function disableTransitionsTemporarily() {
    document.documentElement.classList.add('[&_*]:!transition-none')
    window.setTimeout(() => {
      document.documentElement.classList.remove('[&_*]:!transition-none')
    }, 0)
  }
</script>

<header class="flex items-center justify-between w-full py-4 mx-auto lg:pb-8 gap-16"> 
  <Logo />

  <div class="relative flex justify-around gap-2 items-center">
    <button class="sm:hidden" on:click={toggleMenu}>
      <MenuIcon class="h-6 w-6" />
    </button>
    
    <nav aria-label="Global" class={`${menuOpen ? 'block' : 'hidden'} absolute top-full right-3 w-full sm:relative sm:flex sm:items-center bg-white sm:bg-transparent`}>
      <ul class="flex flex-col sm:flex-row gap-2 text-sm w-full sm:w-auto">
        <MenuItems {navMenu} />
      </ul>
    </nav>


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