<script>
  import { onMount } from 'svelte';
  import { browser } from '$app/environment';

  let currentHash = $state('#profile');
  let avatarFileInput = $state(null);
  let avatarPreview = $state("JD");
  let avatarImageUrl = $state(null);

  onMount(() => {
    const update = () => currentHash = window.location.hash || '#profile';
    update();
    window.addEventListener('hashchange', update);
    return () => window.removeEventListener('hashchange', update);
  });

  function triggerFileUpload() {
    avatarFileInput?.click();
  }

  function handleFileChange(event) {
    const file = event.target.files?.[0];
    if (file) {
      if (!['image/jpeg', 'image/png', 'image/gif'].includes(file.type)) {
        alert('Please upload JPG, PNG, or GIF file only.');
        return;
      }
      if (file.size > 2 * 1024 * 1024) {
        alert('File size must be less than 2MB.');
        return;
      }
      const reader = new FileReader();
      reader.onload = (e) => avatarImageUrl = e.target?.result;
      reader.readAsDataURL(file);
    }
  }

  function removeAvatar() {
    avatarImageUrl = null;
    avatarPreview = "JD";
    if (avatarFileInput) avatarFileInput.value = '';
  }
</script>

{#if currentHash === '#profile'}
<section id="profile" class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
  <div class="px-8 py-6 border-b border-gray-100">
    <h2 class="text-2xl font-bold text-gray-900">Profile & Account</h2>
    <p class="text-base text-gray-500 mt-1">Manage your personal information and account security</p>
  </div>
  <div class="p-8 space-y-8">
    <div class="flex items-center gap-6">
      {#if "/profile.png"}
        <img src={"/profile.png"} alt="Profile" class="w-24 h-24 rounded-full object-cover shadow-lg"/>
      {:else}
        <div class="w-24 h-24 rounded-full bg-gradient-to-br from-blue-400 to-purple-500 flex items-center justify-center text-white text-3xl font-bold shadow-lg">
          {avatarPreview}
        </div>
      {/if}
      <div class="space-y-3">
        <div class="flex gap-3">
          <input bind:this={avatarFileInput} type="file" accept="image/jpeg,image/png,image/gif" onchange={handleFileChange} class="hidden"/>
          <button onclick={triggerFileUpload} class="px-5 py-2.5 bg-gray-900 text-white text-base font-medium rounded-xl hover:bg-gray-800 transition-colors shadow-sm hover:shadow-md cursor-pointer">Change Photo</button>
          <button onclick={removeAvatar} class="px-5 py-2.5 border border-gray-300 text-gray-700 text-base font-medium rounded-xl hover:bg-gray-50 transition-colors cursor-pointer">Remove</button>
        </div>
        <p class="text-sm text-gray-500">JPG, PNG or GIF. Max 2MB.</p>
      </div>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <div class="space-y-2">
        <label class="text-base font-medium text-gray-700">Display Name</label>
        <input type="text" value="Emperor Richard" class="w-full px-4 py-3 text-base border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all bg-gray-50/50"/>
      </div>
      <div class="space-y-2">
        <label class="text-base font-medium text-gray-700">Student ID</label>
        <input type="text" value="SMAK2_2026_CAPO_001" readonly class="w-full px-4 py-3 text-base bg-gray-100 border border-gray-200 rounded-xl text-gray-500 cursor-not-allowed"/>
      </div>
      <div class="space-y-2 md:col-span-2">
        <label class="text-base font-medium text-gray-700">Bio</label>
        <textarea rows="4" class="w-full px-4 py-3 text-base border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all resize-none bg-gray-50/50" placeholder="Tell us about yourself..."></textarea>
      </div>
      <div class="space-y-2 md:col-span-2">
        <label class="text-base font-medium text-gray-700 flex items-center gap-2">Email Address
          <span class="inline-flex items-center px-2.5 py-1 rounded-lg text-sm font-medium bg-green-100 text-green-800">
            <svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"/></svg>
            Verified
          </span>
        </label>
        <input type="email" value="emperor.richard@smak2bpk.penabur.sch.id" class="w-full px-4 py-3 text-base border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all bg-gray-50/50"/>
      </div>
    </div>
    <div class="pt-8 border-t border-gray-100">
      <h3 class="text-lg font-semibold text-gray-900 mb-4">Change Password</h3>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <input type="password" placeholder="Current password" class="w-full px-4 py-3 text-base border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all bg-gray-50/50"/>
        <input type="password" placeholder="New password" class="w-full px-4 py-3 text-base border border-gray-200 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none transition-all bg-gray-50/50"/>
      </div>
    </div>
    <div class="flex justify-end pt-4">
      <button class="px-8 py-3 bg-blue-600 text-white text-base font-semibold rounded-xl hover:bg-blue-700 transition-all shadow-sm hover:shadow-md cursor-pointer">Save Changes</button>
    </div>
  </div>
</section>
{/if}