<script>
  export let navMenu;
  export let toggleMenu;
  import { page } from '$app/stores';
</script>

<style>
  ul {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  @media (min-width: 768px) {
    ul {
      flex-direction: row;
    }
  }
</style>

<ul>
  {#each navMenu as item}
    <li>
      <a
        href={item.link}
        class={`${$page.url.pathname === item.link ? 'rounded-lg bg-teal-100 text-teal-800 dark:bg-teal-900 dark:text-teal-100': 'rounded-lg bg-transparent text-teal-800 dark:bg-transparent dark:text-teal-100'} inline-block px-4 py-2 text-sm rounded font-medium hover:bg-teal-200 hover:text-teal-900 dark:hover:bg-teal-800 dark:hover:text-teal-100 focus:relative transition-colors duration-300`}
        on:click={toggleMenu}
      >
        {item.title}
      </a>
    </li>
  {/each}
  <li>
    <a
      href="mailto:info@ethereumcommons.org"
      class={`${$page.url.pathname === '/contact' ? 'rounded-lg bg-teal-100 text-teal-800 dark:bg-teal-900 dark:text-teal-100': 'rounded-lg bg-transparent text-teal-800 dark:bg-transparent dark:text-teal-100'} inline-block px-4 py-2 text-sm rounded font-medium hover:bg-teal-200 hover:text-teal-900 dark:hover:bg-teal-800 dark:hover:text-teal-100 focus:relative transition-colors duration-300`}
      on:click={toggleMenu}
    >
      Contact
    </a>
  </li>
</ul>