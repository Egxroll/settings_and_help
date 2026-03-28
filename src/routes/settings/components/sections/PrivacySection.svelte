<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#privacy');
  let showName = $state(true);
  let showPhoto = $state(true);
  let showBio = $state(false);

  onMount(() => {
    const update = () => currentHash = window.location.hash || '#privacy';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });
</script>

{#if currentHash === '#privacy'}
<section id="privacy" class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
  <div class="px-8 py-6 border-b border-gray-100">
    <h2 class="text-2xl font-bold text-gray-900">Privacy & Security</h2>
    <p class="text-base text-gray-500 mt-1">Control your visibility and account security</p>
  </div>
  <div class="p-8 space-y-8">
    <div class="space-y-5">
      <h3 class="text-lg font-semibold text-gray-900">Profile Visibility</h3>
      <div class="space-y-4">
        <label class="flex items-center justify-between cursor-pointer group p-4 -mx-4 rounded-xl hover:bg-gray-50 transition-colors">
          <div class="flex-1 pr-4">
            <p class="font-semibold text-gray-900 text-base">Show name to classmates</p>
            <p class="text-sm text-gray-500 mt-1">Your name will appear in discussion forums and group work</p>
          </div>
          <div class="relative inline-flex h-7 w-14 items-center rounded-full transition-colors cursor-pointer {showName ? 'bg-blue-600' : 'bg-gray-300'}">
            <input type="checkbox" bind:checked={showName} class="sr-only"/>
            <span class="inline-block h-5 w-5 transform rounded-full bg-white shadow-md transition-transform {showName ? 'translate-x-8' : 'translate-x-1'}"></span>
          </div>
        </label>
        <label class="flex items-center justify-between cursor-pointer group p-4 -mx-4 rounded-xl hover:bg-gray-50 transition-colors">
          <div class="flex-1 pr-4">
            <p class="font-semibold text-gray-900 text-base">Show profile photo</p>
            <p class="text-sm text-gray-500 mt-1">Display your avatar in class rosters and discussions</p>
          </div>
          <div class="relative inline-flex h-7 w-14 items-center rounded-full transition-colors cursor-pointer {showPhoto ? 'bg-blue-600' : 'bg-gray-300'}">
            <input type="checkbox" bind:checked={showPhoto} class="sr-only"/>
            <span class="inline-block h-5 w-5 transform rounded-full bg-white shadow-md transition-transform {showPhoto ? 'translate-x-8' : 'translate-x-1'}"></span>
          </div>
        </label>
        <label class="flex items-center justify-between cursor-pointer group p-4 -mx-4 rounded-xl hover:bg-gray-50 transition-colors">
          <div class="flex-1 pr-4">
            <p class="font-semibold text-gray-900 text-base">Show bio to classmates</p>
            <p class="text-sm text-gray-500 mt-1">Share your bio information with other students</p>
          </div>
          <div class="relative inline-flex h-7 w-14 items-center rounded-full transition-colors cursor-pointer {showBio ? 'bg-blue-600' : 'bg-gray-300'}">
            <input type="checkbox" bind:checked={showBio} class="sr-only"/>
            <span class="inline-block h-5 w-5 transform rounded-full bg-white shadow-md transition-transform {showBio ? 'translate-x-8' : 'translate-x-1'}"></span>
          </div>
        </label>
      </div>
    </div>
    <div class="border-t border-gray-100 pt-8">
      <div class="flex items-center justify-between">
        <div>
          <h3 class="text-lg font-semibold text-gray-900">Two-Factor Authentication (2FA)</h3>
          <p class="text-base text-gray-500 mt-1">Add an extra layer of security to your account</p>
        </div>
        <button class="px-6 py-3 border border-gray-300 text-gray-700 text-base font-medium rounded-xl hover:bg-gray-50 transition-colors hover:border-gray-400 cursor-pointer">Enable 2FA</button>
      </div>
    </div>
    <div class="flex justify-end">
      <button class="px-8 py-3 bg-blue-600 text-white text-base font-semibold rounded-xl hover:bg-blue-700 transition-all shadow-sm hover:shadow-md cursor-pointer">Save Privacy Settings</button>
    </div>
  </div>
</section>
{/if}