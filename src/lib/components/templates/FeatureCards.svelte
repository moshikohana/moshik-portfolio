<script context="module" lang="ts">
  export interface Feature {
    icon: any;
    iconColor: string;
    iconBgColor: string;
    title: string;
    description: string;
  }
</script>

<script lang="ts">
  import { fly } from 'svelte/transition';
  
  export let features: Feature[] = [];
  export let title = "Powerful Features";
  export let titleGradient = "from-indigo-400 to-cyan-400";
  export let columns = 3;
</script>

<section class="py-16 px-4 sm:px-6 lg:px-8 bg-slate-800/50">
  <div class="max-w-7xl mx-auto">
    <h2 class="text-2xl font-bold text-center mb-12">
      <span class="bg-clip-text text-transparent bg-gradient-to-r {titleGradient}">
        {title}
      </span>
    </h2>
    
    <div class="grid grid-cols-1 md:grid-cols-{columns} gap-8">
      {#each features as feature, i}
        <div 
          class="feature-card bg-slate-700/50 p-6 rounded-xl border border-slate-600 backdrop-blur-sm"
          in:fly={{ y: 20, duration: 400, delay: i * 100 }}
        >
          <div class="w-12 h-12 rounded-lg {feature.iconBgColor} flex items-center justify-center mb-4">
            <svelte:component this={feature.icon} size={24} class="{feature.iconColor}" />
          </div>
          <h3 class="text-xl font-semibold mb-2">{feature.title}</h3>
          <p class="text-slate-300">{feature.description}</p>
        </div>
      {/each}
    </div>
  </div>
</section> 