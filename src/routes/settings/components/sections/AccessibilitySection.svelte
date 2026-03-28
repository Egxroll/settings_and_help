<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#accessibility');
  let showMotion = $state(false);

  onMount(() => {
    const update = () => currentHash = window.location.hash || '#accessibility';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });
</script>

{#if currentHash === '#accessibility'}
<section id="accessibility" class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
  <div class="px-8 py-6 border-b border-gray-100">
    <h2 class="text-2xl font-bold text-gray-900">Accessibility</h2>
    <p class="text-base text-gray-500 mt-1">Customize your viewing experience</p>
  </div>
  <div class="p-8 space-y-8">
    <div class="space-y-5">
      <div class="flex items-center justify-between">
        <label class="text-lg font-semibold text-gray-900">Font Size</label>
        <span class="text-base text-gray-500 font-medium">100%</span>
      </div>
      <div class="flex items-center gap-6">
        <span class="text-base text-gray-500 font-medium">A</span>
        <input type="range" min="85" max="125" value="100" class="flex-1 h-3 bg-gray-200 rounded-full appearance-none cursor-pointer accent-blue-600 hover:accent-blue-700"/>
        <span class="text-xl text-gray-500 font-medium">A</span>
      </div>
      <div class="flex justify-between text-sm text-gray-400 px-1">
        <span>85%</span>
        <span>100%</span>
        <span>125%</span>
      </div>
    </div>
    <label class="flex items-center justify-between cursor-pointer group py-5 border-t border-gray-100 hover:bg-gray-50 rounded-xl px-4 -mx-4 transition-colors">
      <div>
        <p class="font-semibold text-gray-900 text-lg">Reduced Motion</p>
        <p class="text-base text-gray-500 mt-1">Minimize animations throughout the interface</p>
      </div>
      <div class="relative inline-flex h-7 w-14 items-center rounded-full transition-colors cursor-pointer {showMotion ? 'bg-blue-600' : 'bg-gray-300'}">
        <input type="checkbox" bind:checked={showMotion} class="sr-only"/>
        <span class="inline-block h-5 w-5 transform rounded-full bg-white shadow-md transition-transform {showMotion ? 'translate-x-8' : 'translate-x-1'}"></span>
      </div>
    </label>
    <div class="flex justify-end pt-4">
      <button class="px-8 py-3 bg-blue-600 text-white text-base font-semibold rounded-xl hover:bg-blue-700 transition-all shadow-sm hover:shadow-md cursor-pointer">Save Accessibility Settings</button>
    </div>
  </div>
</section>
{/if}