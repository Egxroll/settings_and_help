<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#accessibility');
  let showMotion = $state(false);
  let fontSize = $state('normal');

  onMount(() => {
    const update = () => currentHash = window.location.hash || '#accessibility';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });

  function handleSaveAccessibility() {
    // TODO: Backend by Anoki
  }
</script>

{#if currentHash === '#accessibility'}
<section id="accessibility" class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl overflow-hidden text-sm text-slate-900 dark:text-slate-100">
  <div class="px-8 py-6 border-b border-slate-200 dark:border-slate-800">
    <h2 class="text-2xl font-bold">Accessibility</h2>
    <p class="mt-1 text-slate-500 dark:text-slate-400">Customize your viewing experience</p>
  </div>
  
  <div class="p-8 flex flex-col gap-8">
    <!-- Font Size Selection -->
    <div class="flex flex-col gap-4">
      <label class="font-semibold text-base">Font Size</label>
      <div class="grid grid-cols-3 gap-3">
        <button 
          onclick={() => fontSize = 'small'}
          class="flex flex-col items-center gap-2 p-4 border-2 rounded-xl cursor-pointer transition-all duration-200 {fontSize === 'small' ? 'border-blue-500 dark:border-blue-400 bg-blue-50 dark:bg-blue-900/20' : 'border-slate-200 dark:border-slate-700 hover:border-slate-300 dark:hover:border-slate-600'}"
        >
          <span class="text-sm font-medium text-slate-500 dark:text-slate-400">A</span>
          <span class="text-xs font-medium {fontSize === 'small' ? 'text-blue-600 dark:text-blue-400' : 'text-slate-500 dark:text-slate-400'}">Small</span>
        </button>
        
        <button 
          onclick={() => fontSize = 'normal'}
          class="flex flex-col items-center gap-2 p-4 border-2 rounded-xl cursor-pointer transition-all duration-200 {fontSize === 'normal' ? 'border-blue-500 dark:border-blue-400 bg-blue-50 dark:bg-blue-900/20' : 'border-slate-200 dark:border-slate-700 hover:border-slate-300 dark:hover:border-slate-600'}"
        >
          <span class="text-base font-medium text-slate-700 dark:text-slate-300">A</span>
          <span class="text-xs font-medium {fontSize === 'normal' ? 'text-blue-600 dark:text-blue-400' : 'text-slate-500 dark:text-slate-400'}">Normal</span>
        </button>
        
        <button 
          onclick={() => fontSize = 'big'}
          class="flex flex-col items-center gap-2 p-4 border-2 rounded-xl cursor-pointer transition-all duration-200 {fontSize === 'big' ? 'border-blue-500 dark:border-blue-400 bg-blue-50 dark:bg-blue-900/20' : 'border-slate-200 dark:border-slate-700 hover:border-slate-300 dark:hover:border-slate-600'}"
        >
          <span class="text-xl font-medium text-slate-900 dark:text-slate-100">A</span>
          <span class="text-xs font-medium {fontSize === 'big' ? 'text-blue-600 dark:text-blue-400' : 'text-slate-500 dark:text-slate-400'}">Big</span>
        </button>
      </div>
    </div>

    <!-- Reduced Motion Toggle -->
    <label class="flex items-center justify-between py-4 px-4 -mx-4 border-t border-slate-200 dark:border-slate-800 rounded-xl cursor-pointer hover:bg-slate-50 dark:hover:bg-slate-800/50">
      <div class="flex flex-col gap-1">
        <p class="font-semibold text-base">Reduced Motion</p>
        <p class="text-xs text-slate-500 dark:text-slate-400">Minimize animations throughout the interface</p>
      </div>
      <button 
        onclick={() => showMotion = !showMotion}
        class="relative inline-flex h-7 w-14 items-center rounded-full cursor-pointer {showMotion ? 'bg-blue-600 dark:bg-blue-500' : 'bg-slate-200 dark:bg-slate-800'}"
      >
        <span class="inline-block h-5 w-5 rounded-full bg-white dark:bg-slate-400 shadow-md transition-transform duration-200 {showMotion ? 'translate-x-8' : 'translate-x-1'}"></span>
      </button>
    </label>

    <!-- Save Button -->
    <div class="flex justify-end pt-4">
      <button onclick={handleSaveAccessibility} class="px-8 py-3 bg-blue-600 text-white font-semibold rounded-xl cursor-pointer hover:bg-blue-700 shadow-sm hover:shadow-md">
        Save Accessibility Settings
      </button>
    </div>
  </div>
</section>
{/if}