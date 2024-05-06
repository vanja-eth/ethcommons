<script>
  export let image;
  export let alt;
  export let title;
  export let description;
</script>

<div class="flex flex-col items-left">
  <img src={image} alt={alt} class="mb-4 h-24 w-24 rounded-full">
  <div>
    <h3 class="text-xl font-bold text-teal-700 dark:text-white pb-2">{title}</h3>
    <p class="text-teal-600 dark:text-white">{description}</p>
  </div>
</div>