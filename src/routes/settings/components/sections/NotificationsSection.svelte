<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#notifications');
  onMount(() => {
    const update = () => currentHash = window.location.hash || '#notifications';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });
</script>

{#if currentHash === '#notifications'}
<section id="notifications" class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
  <div class="px-8 py-6 border-b border-gray-100">
    <h2 class="text-2xl font-bold text-gray-900">Notifications</h2>
    <p class="text-base text-gray-500 mt-1">Choose what you want to be notified about</p>
  </div>
  <div class="p-8">
    <div class="space-y-4">
      <div class="grid grid-cols-12 gap-4 pb-3 border-b border-gray-200 text-base font-medium text-gray-500">
        <div class="col-span-6">Notification Type</div>
        <div class="col-span-3 text-center">In-App</div>
        <div class="col-span-3 text-center">Email</div>
      </div>
      <div class="grid grid-cols-12 gap-4 items-center py-4 hover:bg-gray-50 rounded-xl px-3 -mx-3 transition-colors">
        <div class="col-span-6">
          <p class="font-semibold text-gray-900 text-base">Assignment/Material/Quiz announcements</p>
          <p class="text-sm text-gray-500 mt-1">New content posted by instructors</p>
        </div>
        <div class="col-span-3 flex justify-center">
          <input type="checkbox" checked class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
        <div class="col-span-3 flex justify-center">
          <input type="checkbox" checked class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
      </div>
      <div class="grid grid-cols-12 gap-4 items-start py-4 hover:bg-gray-50 rounded-xl px-3 -mx-3 transition-colors">
        <div class="col-span-6">
          <p class="font-semibold text-gray-900 text-base">Assignment due soon</p>
          <p class="text-sm text-gray-500 mt-1">Get notified before deadline</p>
        </div>
        <div class="col-span-3 flex justify-center pt-1">
          <input type="checkbox" checked class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
        <div class="col-span-3 flex justify-center pt-1">
          <input type="checkbox" class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
        <div class="col-span-12 mt-2">
          <label class="text-sm text-gray-600 mb-1 block">Notify me:</label>
          <select class="text-sm border border-gray-200 rounded-lg px-3 py-2 bg-gray-50/50 cursor-pointer hover:bg-white transition-colors w-48">
            <option>24 hours before</option>
            <option>48 hours before</option>
            <option>1 week before</option>
          </select>
        </div>
      </div>
      <div class="grid grid-cols-12 gap-4 items-center py-4 hover:bg-gray-50 rounded-xl px-3 -mx-3 transition-colors">
        <div class="col-span-6">
          <p class="font-semibold text-gray-900 text-base">Grades released</p>
          <p class="text-sm text-gray-500 mt-1">When your submissions are graded</p>
        </div>
        <div class="col-span-3 flex justify-center">
          <input type="checkbox" checked class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
        <div class="col-span-3 flex justify-center">
          <input type="checkbox" checked class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
      </div>
      <div class="grid grid-cols-12 gap-4 items-center py-4 hover:bg-gray-50 rounded-xl px-3 -mx-3 transition-colors">
        <div class="col-span-6">
          <p class="font-semibold text-gray-900 text-base">Teacher feedback & messages</p>
          <p class="text-sm text-gray-500 mt-1">Direct communications from instructors</p>
        </div>
        <div class="col-span-3 flex justify-center">
          <input type="checkbox" checked class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
        <div class="col-span-3 flex justify-center">
          <input type="checkbox" checked class="w-5 h-5 text-blue-600 rounded-lg border-gray-300 focus:ring-blue-500 cursor-pointer"/>
        </div>
      </div>
    </div>
    <div class="flex justify-end pt-8 mt-8 border-t border-gray-100">
      <button class="px-8 py-3 bg-blue-600 text-white text-base font-semibold rounded-xl hover:bg-blue-700 transition-all shadow-sm hover:shadow-md cursor-pointer">Save Notification Settings</button>
    </div>
  </div>
</section>
{/if}