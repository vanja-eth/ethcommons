<script>
  import ArrowRightIcon from '$lib/components/ArrowRightIcon.svelte';
  import EthSvg from '$lib/components/eth_svg.svelte';
  import { bio, name } from '$lib/info.js';
  import ListItem from '$lib/components/ListItem.svelte';
  import { items } from '$lib/items.js';
  import CommunityMission from '$lib/components/CommunityMission.svelte';
  import { communityMissionData } from '$lib/communityMissionData.js';
</script>

<svelte:head>
  <title>{name} | Ethereum for Social Good</title>
  <meta name="description" content={bio} />
</svelte:head>

<section class="w-full">
  <div class="container mx-auto px-4 py-8">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8" style="grid-template-columns: 60% 40%;">
      <div>
        <h1 class="text-4xl font-bold mb-4 my-8">Ethereum for social good</h1>
        <p class="text-lg mb-4">{bio}</p>
      </div>
      <div>
        <div class="mr-8 bg-zinc-600 dark:bg-zinc-300 hover:bg-zinc-700 dark:hover:bg-zinc-200 p-6 rounded-3xl shadow-lg mt-10 transition-colors duration-300">          
          <div class=" flex items-center">
            <EthSvg class="w-6 h-6 fill-current text-white dark:text-zinc-800" />
            <h2 class="text-2xl px-1 font-bold text-zinc-100 dark:text-zinc-900">Ethereum</h2>
          </div>

            <p class="text-m text-zinc-400 dark:text-zinc-600 py-2">/ɪˈθɪərɪəm/ [Ee-thee-ree-um] <span class="text-m font-medium italic">(noun)</span></p>
            <p class="text-m text-zinc-300 dark:text-zinc-800">
                A global, open-source computing platform where decentralized applications, smart contracts, and digital assets are built and shared, facilitating the emergence of a transparent, permissionless, and trustless economy.
            </p>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="p-4">
  <section class="w-full bg-gradient-to-t from-white to-teal-100 dark:from-black dark:to-zinc-800 rounded-3xl py-7 p-4">
    <div class="container mx-auto">
      <h1 class="text-4xl text-teal-800 font-bold mx-4">Our Community Mission</h1>
    </div>

    <section class="p-8">
      <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-12 text-left">
        {#each communityMissionData as mission}
          <CommunityMission 
            image={mission.image} 
            alt={mission.alt} 
            title={mission.title} 
            description={mission.description} 
          />
        {/each}
      </div>
    </section>
  </section>
</div>


<section class="w-full py-7 p-4">
  <div class="mb-8 mt-8">
    <h2 class="text-4xl font-bold mb-2">Why Ethereum?</h2>
  </div>
  <ul class="grid grid-cols-1 sm:grid-cols-2 gap-x-8 gap-y-8 mb-12">
    {#each items as item (item.title)}
      <ListItem title={item.title} description={item.description} svgPath={item.svgPath} className="faint-shadow transition-shadow duration-300" />
    {/each}
  </ul>
</section>