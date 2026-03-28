<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#connected');

  onMount(() => {
    const update = () => currentHash = window.location.hash || '#connected';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });
</script>

{#if currentHash === '#connected'}
<section id="connected" class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
  <div class="px-8 py-6 border-b border-gray-100">
    <h2 class="text-2xl font-bold text-gray-900">Connected Accounts</h2>
    <p class="text-base text-gray-500 mt-1">Link external services for enhanced functionality</p>
  </div>
  <div class="p-8 space-y-5">
    <div class="flex items-center justify-between p-6 border border-gray-200 rounded-xl hover:border-gray-300 hover:shadow-sm transition-all">
      <div class="flex items-center gap-5">
        <div class="w-14 h-14 bg-blue-100 rounded-xl flex items-center justify-center">
          <svg class="w-7 h-7 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/></svg>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-lg">Calendar Sync</p>
          <p class="text-base text-gray-500">Auto-add assignment deadlines to your calendar</p>
        </div>
      </div>
      <button class="px-6 py-3 border border-gray-300 text-gray-700 text-base font-medium rounded-xl hover:bg-gray-50 transition-colors hover:border-gray-400 cursor-pointer">Connect</button>
    </div>
    <div class="flex items-center justify-between p-6 border border-gray-200 rounded-xl hover:border-gray-300 hover:shadow-sm transition-all">
      <div class="flex items-center gap-5">
        <div class="w-14 h-14 bg-red-50 rounded-xl flex items-center justify-center">
          <svg class="w-7 h-7 text-red-600" viewBox="0 0 24 24" fill="currentColor"><path d="M12.545,10.239v3.821h5.445c-0.712,2.315-2.647,3.972-5.445,3.972c-3.332,0-6.033-2.701-6.033-6.032s2.701-6.032,6.033-6.032c1.498,0,2.866,0.549,3.921,1.453l2.814-2.814C17.503,2.988,15.139,2,12.545,2C7.021,2,2.543,6.477,2.543,12s4.478,10,10.002,10c8.396,0,10.249-7.85,9.426-11.748L12.545,10.239z"/></svg>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-lg">Google Account</p>
          <p class="text-base text-gray-500">Sign in with Google and sync Google Calendar</p>
        </div>
      </div>
      <button class="px-6 py-3 border border-gray-300 text-gray-700 text-base font-medium rounded-xl hover:bg-gray-50 transition-colors hover:border-gray-400 cursor-pointer">Connect</button>
    </div>
    <div class="flex items-center justify-between p-6 border border-gray-200 rounded-xl hover:border-gray-300 hover:shadow-sm transition-all">
      <div class="flex items-center gap-5">
        <div class="w-14 h-14 bg-blue-50 rounded-xl flex items-center justify-center">
          <svg class="w-7 h-7 text-blue-700" viewBox="0 0 24 24" fill="currentColor"><path d="M0 0h11.377v11.372H0zm12.623 0H24v11.372H12.623zM0 12.623h11.377V24H0zm12.623 0H24V24H12.623z"/></svg>
        </div>
        <div>
          <p class="font-semibold text-gray-900 text-lg">Microsoft Account</p>
          <p class="text-base text-gray-500">Sign in with Microsoft and sync Outlook Calendar</p>
        </div>
      </div>
      <button class="px-6 py-3 border border-gray-300 text-gray-700 text-base font-medium rounded-xl hover:bg-gray-50 transition-colors hover:border-gray-400 cursor-pointer">Connect</button>
    </div>
  </div>
</section>
{/if}