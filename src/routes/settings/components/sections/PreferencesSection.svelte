<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#preferences');
  onMount(() => {
    const update = () => currentHash = window.location.hash || '#preferences';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });
</script>

{#if currentHash === '#preferences'}
<section id="preferences" class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
  <div class="px-8 py-6 border-b border-gray-100">
    <h2 class="text-2xl font-bold text-gray-900">App Preferences</h2>
    <p class="text-base text-gray-500 mt-1">Customize your experience</p>
  </div>
  <div class="p-8 space-y-8">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div class="space-y-3">
        <label class="text-base font-medium text-gray-700">Time Zone</label>
        <select class="w-full px-4 py-3 text-base border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all bg-gray-50/50 cursor-pointer">
          <option value="UTC+07:00">WIB (Jakarta, Bangkok, Hanoi) - UTC+07:00</option>
          <option value="UTC+08:00">WITA (Singapore, Kuala Lumpur, Manila) - UTC+08:00</option>
          <option value="UTC+08:00">WITA (Hong Kong, Taipei, Shanghai) - UTC+08:00</option>
          <option value="UTC+09:00">WIT (Tokyo, Seoul, Jayapura) - UTC+09:00</option>
        </select>
        <p class="text-sm text-gray-500">Used for assignment due dates and scheduling</p>
      </div>
      <div class="space-y-3">
        <label class="text-base font-medium text-gray-700">Date Format</label>
        <select class="w-full px-4 py-3 text-base border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all bg-gray-50/50 cursor-pointer">
          <option>DD/MM/YYYY (12-hour)</option>
          <option>DD/MM/YYYY (24-hour)</option>
          <option>MM/DD/YYYY (12-hour)</option>
          <option>MM/DD/YYYY (24-hour)</option>
          <option>YYYY-MM-DD (24-hour)</option>
        </select>
      </div>
    </div>
    <div class="flex justify-end">
      <button class="px-8 py-3 bg-blue-600 text-white text-base font-semibold rounded-xl hover:bg-blue-700 transition-all shadow-sm hover:shadow-md cursor-pointer">Save Preferences</button>
    </div>
  </div>
</section>
{/if}