<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#preferences');
  let selectedTheme = $state('system');
  
  onMount(() => {
    const update = () => currentHash = window.location.hash || '#preferences';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });

  function handleSavePreferences() {
    // TODO: Backend by Anoki
  }
</script>

{#if currentHash === '#preferences'}
<section id="preferences" class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl overflow-hidden text-sm text-slate-900 dark:text-slate-100">
  <div class="px-8 py-6 border-b border-slate-200 dark:border-slate-800">
    <h2 class="text-2xl font-bold">App Preferences</h2>
    <p class="mt-1 text-slate-500 dark:text-slate-400">Customize your experience</p>
  </div>
  
  <div class="p-8 flex flex-col gap-8">
    <!-- Theme Selection -->
    <div class="flex flex-col gap-3">
      <label class="font-medium">Theme</label>
      <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
        <button 
          onclick={() => selectedTheme = 'system'}
          class="flex items-center gap-3 p-4 border rounded-xl cursor-pointer {selectedTheme === 'system' ? 'bg-slate-50 dark:bg-slate-800 border-blue-500 dark:border-blue-400' : 'bg-white dark:bg-slate-900 border-slate-200 dark:border-slate-800 hover:bg-slate-50 dark:hover:bg-slate-800'}"
        >
          <div class="w-8 h-8 bg-slate-100 dark:bg-slate-700 rounded-lg flex items-center justify-center">
            <svg class="w-4 h-4 text-slate-600 dark:text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
          </div>
          <div class="text-left">
            <p class="font-medium">System Default</p>
            <p class="text-xs text-slate-500 dark:text-slate-400">Follow device setting</p>
          </div>
        </button>
        
        <button 
          onclick={() => selectedTheme = 'light'}
          class="flex items-center gap-3 p-4 border rounded-xl cursor-pointer {selectedTheme === 'light' ? 'bg-slate-50 dark:bg-slate-800 border-blue-500 dark:border-blue-400' : 'bg-white dark:bg-slate-900 border-slate-200 dark:border-slate-800 hover:bg-slate-50 dark:hover:bg-slate-800'}"
        >
          <div class="w-8 h-8 bg-yellow-100 rounded-lg flex items-center justify-center">
            <svg class="w-4 h-4 text-yellow-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"/></svg>
          </div>
          <div class="text-left">
            <p class="font-medium">Light</p>
            <p class="text-xs text-slate-500 dark:text-slate-400">Always light mode</p>
          </div>
        </button>
        
        <button 
          onclick={() => selectedTheme = 'dark'}
          class="flex items-center gap-3 p-4 border rounded-xl cursor-pointer {selectedTheme === 'dark' ? 'bg-slate-50 dark:bg-slate-800 border-blue-500 dark:border-blue-400' : 'bg-white dark:bg-slate-900 border-slate-200 dark:border-slate-800 hover:bg-slate-50 dark:hover:bg-slate-800'}"
        >
          <div class="w-8 h-8 bg-indigo-100 dark:bg-indigo-900/30 rounded-lg flex items-center justify-center">
            <svg class="w-4 h-4 text-indigo-600 dark:text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"/></svg>
          </div>
          <div class="text-left">
            <p class="font-medium">Dark</p>
            <p class="text-xs text-slate-500 dark:text-slate-400">Always dark mode</p>
          </div>
        </button>
      </div>
    </div>

    <!-- Regional Settings -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 pt-6 border-t border-slate-200 dark:border-slate-800">
      <div class="flex flex-col gap-3">
        <label class="font-medium">Time Zone</label>
        <select class="w-full px-4 py-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500 cursor-pointer">
          <option value="GMT+07:00">Western Indonesia Time (WIB) - GMT+07:00</option>
          <option value="GMT+08:00">Central Indonesia Time (WITA) - GMT+08:00</option>
          <option value="GMT+09:00">Eastern Indonesia Time (WIT) - GMT+09:00</option>
        </select>
        <p class="text-xs text-slate-500 dark:text-slate-400">Used for assignment due dates and scheduling</p>
      </div>
      
      <div class="flex flex-col gap-3">
        <label class="font-medium">Date Format</label>
        <select class="w-full px-4 py-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500 cursor-pointer">
          <option>DD/MM/YYYY (12-hour)</option>
          <option>DD/MM/YYYY (24-hour)</option>
          <option>MM/DD/YYYY (12-hour)</option>
          <option>MM/DD/YYYY (24-hour)</option>
          <option>YYYY-MM-DD (24-hour)</option>
        </select>
      </div>
    </div>
    
    <div class="flex justify-end pt-4">
      <button onclick={handleSavePreferences} class="px-8 py-3 bg-blue-600 text-white font-semibold rounded-xl cursor-pointer hover:bg-blue-700 shadow-sm hover:shadow-md">
        Save Preferences
      </button>
    </div>
  </div>
</section>
{/if}