<script>
  import { onMount } from 'svelte';
  let currentHash = $state('#notifications');
  
  let assignmentInApp = $state(false);
  let assignmentEmail = $state(true);
  let dueSoonInApp = $state(true);
  let dueSoonEmail = $state(false);
  let dueSoonTiming = $state('24 hours before');
  let gradesInApp = $state(true);
  let gradesEmail = $state(true);
  let feedbackInApp = $state(false);
  let feedbackEmail = $state(false);

  onMount(() => {
    const update = () => currentHash = window.location.hash || '#notifications';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });

  function handleSaveNotifications() {
    // TODO: Backend by Anoki
  }
</script>

{#if currentHash === '#notifications'}
<section id="notifications" class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl overflow-hidden text-sm text-slate-900 dark:text-slate-100">
  <div class="px-8 py-6 border-b border-slate-200 dark:border-slate-800">
    <h2 class="text-2xl font-bold">Notifications</h2>
    <p class="mt-1 text-slate-500 dark:text-slate-400">Choose what you want to be notified about</p>
  </div>
  
  <div class="p-8 flex flex-col gap-6">
    <!-- Header Row -->
    <div class="grid grid-cols-12 gap-4 pb-3 border-b border-slate-200 dark:border-slate-800 text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">
      <div class="col-span-6">Notification Type</div>
      <div class="col-span-3 text-center">In-App</div>
      <div class="col-span-3 text-center">Email</div>
    </div>

    <!-- Assignment/Material/Quiz -->
    <div class="grid grid-cols-12 gap-4 items-center py-3 px-3 -mx-3 rounded-xl hover:bg-slate-50 dark:hover:bg-slate-800/50">
      <div class="col-span-6 flex flex-col gap-1">
        <p class="font-semibold text-base">Assignment/Material/Quiz announcements</p>
        <p class="text-xs text-slate-500 dark:text-slate-400">New content posted by instructors</p>
      </div>
      <div class="col-span-3 flex justify-center">
        <button 
          onclick={() => assignmentInApp = !assignmentInApp}
          class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {assignmentInApp ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
        >
          {#if assignmentInApp}
            <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
          {/if}
        </button>
      </div>
      <div class="col-span-3 flex justify-center">
        <button 
          onclick={() => assignmentEmail = !assignmentEmail}
          class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {assignmentEmail ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
        >
          {#if assignmentEmail}
            <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
          {/if}
        </button>
      </div>
    </div>

    <!-- Assignment Due Soon -->
    <div class="flex flex-col gap-3 py-3 px-3 -mx-3 rounded-xl hover:bg-slate-50 dark:hover:bg-slate-800/50">
      <div class="grid grid-cols-12 gap-4 items-center">
        <div class="col-span-6 flex flex-col gap-1">
          <p class="font-semibold text-base">Assignment due soon</p>
          <p class="text-xs text-slate-500 dark:text-slate-400">Get notified before deadline</p>
        </div>
        <div class="col-span-3 flex justify-center">
          <button 
            onclick={() => dueSoonInApp = !dueSoonInApp}
            class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {dueSoonInApp ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
          >
            {#if dueSoonInApp}
              <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
            {/if}
          </button>
        </div>
        <div class="col-span-3 flex justify-center">
          <button 
            onclick={() => dueSoonEmail = !dueSoonEmail}
            class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {dueSoonEmail ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
          >
            {#if dueSoonEmail}
              <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
            {/if}
          </button>
        </div>
      </div>
      <div class="col-span-12">
        <label class="block mb-1 text-xs text-slate-500 dark:text-slate-400">Notify me:</label>
        <select bind:value={dueSoonTiming} class="w-48 px-3 py-2 text-sm bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-lg cursor-pointer hover:bg-white dark:hover:bg-slate-700 outline-none focus:ring-2 focus:ring-blue-500">
          <option>24 hours before</option>
          <option>48 hours before</option>
          <option>1 week before</option>
        </select>
      </div>
    </div>

    <!-- Grades Released -->
    <div class="grid grid-cols-12 gap-4 items-center py-3 px-3 -mx-3 rounded-xl hover:bg-slate-50 dark:hover:bg-slate-800/50">
      <div class="col-span-6 flex flex-col gap-1">
        <p class="font-semibold text-base">Grades released</p>
        <p class="text-xs text-slate-500 dark:text-slate-400">When your submissions are graded</p>
      </div>
      <div class="col-span-3 flex justify-center">
        <button 
          onclick={() => gradesInApp = !gradesInApp}
          class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {gradesInApp ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
        >
          {#if gradesInApp}
            <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
          {/if}
        </button>
      </div>
      <div class="col-span-3 flex justify-center">
        <button 
          onclick={() => gradesEmail = !gradesEmail}
          class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {gradesEmail ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
        >
          {#if gradesEmail}
            <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
          {/if}
        </button>
      </div>
    </div>

    <!-- Teacher Feedback -->
    <div class="grid grid-cols-12 gap-4 items-center py-3 px-3 -mx-3 rounded-xl hover:bg-slate-50 dark:hover:bg-slate-800/50">
      <div class="col-span-6 flex flex-col gap-1">
        <p class="font-semibold text-base">Teacher feedback & messages</p>
        <p class="text-xs text-slate-500 dark:text-slate-400">Direct communications from instructors</p>
      </div>
      <div class="col-span-3 flex justify-center">
        <button 
          onclick={() => feedbackInApp = !feedbackInApp}
          class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {feedbackInApp ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
        >
          {#if feedbackInApp}
            <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
          {/if}
        </button>
      </div>
      <div class="col-span-3 flex justify-center">
        <button 
          onclick={() => feedbackEmail = !feedbackEmail}
          class="w-6 h-6 flex items-center justify-center border-2 rounded cursor-pointer {feedbackEmail ? 'bg-blue-600 dark:bg-blue-500 border-blue-600 dark:border-blue-500' : 'bg-white dark:bg-slate-800 border-slate-300 dark:border-slate-600 hover:border-slate-400 dark:hover:border-slate-500'}"
        >
          {#if feedbackEmail}
            <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/></svg>
          {/if}
        </button>
      </div>
    </div>

    <!-- Save Button -->
    <div class="flex justify-end pt-6 border-t border-slate-200 dark:border-slate-800">
      <button onclick={handleSaveNotifications} class="px-8 py-3 bg-blue-600 text-white font-semibold rounded-xl cursor-pointer hover:bg-blue-700 shadow-sm hover:shadow-md">
        Save Notification Settings
      </button>
    </div>
  </div>
</section>
{/if}