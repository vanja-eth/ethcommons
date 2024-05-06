<script>
  import { navMenu } from '$lib/info'
  import MoonIcon from 'heroicons-svelte/solid/MoonIcon.svelte'
  import SunIcon from 'heroicons-svelte/solid/SunIcon.svelte'
  import { browser } from '$app/environment'
  import { page } from '$app/stores';
  import { name } from '$lib/info'

  let toggleMenu = false;
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
  <a class="flex items-center font-bold dark:text-zinc-200 text-zinc-700" href="/">
    <img src="media/logo.png" alt="Ethereum Commons Logo" class="h-14 w-auto mr-4 object-contain" />
    <div class="flex flex-col items-start">
      <span class="text-xl font-bold offset-first-line tight-space-y">eth</span>
      <span class="text-xl font-bold tight-space-y">commons</span>
      <span class="text-xl font-light tight-space-y">.org</span>
    </div>
  </a>

  <div class="flex justify-around gap-2 items-center">
    <div class="sm:flex hidden justify-center p-1 relative sm:w-auto sm:-space-x-px overflow-hidden sm:rounded">
      <nav aria-label="Global">
        <ul class="flex items-center gap-2 text-sm">
          {#each navMenu as item}
          <li>
            <a
              href={item.link}
              class={`${$page.url.pathname === item.link ? 'rounded-lg bg-teal-100 text-teal-800 dark:bg-teal-900 dark:text-teal-100': 'rounded-lg bg-transparent text-teal-800 dark:bg-transparent dark:text-teal-100'} inline-block px-4 py-2 text-sm rounded font-medium hover:bg-teal-200 hover:text-teal-900 dark:hover:bg-teal-800 dark:hover:text-teal-100 focus:relative transition-colors duration-300` }
            >
              {item.title}
            </a>
          </li>
        {/each}
        <li>
          <a
            href="mailto:info@ethereumcommons.org"
            class={`${$page.url.pathname === '/contact' ? 'rounded-lg bg-teal-100 text-teal-800 dark:bg-teal-900 dark:text-teal-100': 'rounded-lg bg-transparent text-teal-800 dark:bg-transparent dark:text-teal-100'} inline-block px-4 py-2 text-sm rounded font-medium hover:bg-teal-200 hover:text-teal-900 dark:hover:bg-teal-800 dark:hover:text-teal-100 focus:relative transition-colors duration-300`}
          >
            Contact
          </a>
        </li>
          </ul>
      </nav>
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