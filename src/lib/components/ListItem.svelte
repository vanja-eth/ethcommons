<script>
  export let title = '';
  export let description = '';
  export let svgPath = '';
  export let className = '';  
</script>

<li class="rounded-2xl border border-zinc-200 p-6 dark:border-zinc-700 {className}">
  <h2 class="flex text-lg font-semibold text-zinc-700 dark:text-zinc-100">
    <svg class="w-6 h-6 text-zinc-700 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
      <path stroke="currentColor" stroke-linecap="round" stroke-width="2" d={svgPath} />
    </svg>
    <span class="ml-3">{title}</span>
  </h2>
  <p class="mt-5 dark:text-zinc-50 text-zinc-500">{description}</p>
</li>