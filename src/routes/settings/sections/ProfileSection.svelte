<script>
  import { onMount } from 'svelte';
  import { browser } from '$app/environment';
  import { goto } from '$app/navigation';

  let currentHash = $state('#profile');
  let avatarFileInput = $state(null);
  let avatarImageUrl = $state("/profile.png");
  let showDeleteModal = $state(false);
  let showEmailModal = $state(false);
  let showEmailSuccess = $state(false);
  let showPasswordSuccess = $state(false);
  let newEmail = $state('');
  let emailPassword = $state('');

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
      // TODO: Backend by Anoki
      const reader = new FileReader();
      reader.onload = (e) => avatarImageUrl = e.target?.result;
      reader.readAsDataURL(file);
    }
  }

  function removeAvatar() {
    // TODO: Backend by Anoki
    avatarImageUrl = "/profile.png";
    if (avatarFileInput) avatarFileInput.value = '';
  }

  function confirmDelete() {
    // TODO: Backend by Anoki
    showDeleteModal = false;
    goto('/signup');
  }

  function handleEmailChange() {
    // TODO: Backend by Anoki
    showEmailModal = false;
    newEmail = '';
    emailPassword = '';
    showEmailSuccess = true;
    setTimeout(() => showEmailSuccess = false, 5000);
  }

  function handlePasswordUpdate() {
    // TODO: Backend by Anoki
    showPasswordSuccess = true;
    setTimeout(() => showPasswordSuccess = false, 5000);
  }
</script>

{#if currentHash === '#profile'}
<section id="profile" class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl overflow-hidden text-sm text-slate-900 dark:text-slate-100">
  <div class="px-8 py-6 border-b border-slate-200 dark:border-slate-800">
    <h2 class="text-2xl font-bold">Profile & Account</h2>
    <p class="mt-1 text-slate-500 dark:text-slate-400">Manage your personal information and account security</p>
  </div>
  
  <div class="p-8 flex flex-col gap-8">
    <!-- Identity Header -->
    <div class="flex items-center gap-6">
      <img src={avatarImageUrl} alt="Profile" class="w-24 h-24 bg-slate-100 dark:bg-slate-800 rounded-full object-cover shadow-lg"/>
      <div>
        <h3 class="text-xl font-bold">Emperor Richard</h3>
        <p class="text-slate-500 dark:text-slate-400">Student Account</p>
      </div>
    </div>

    <!-- Photo Controls -->
    <div class="flex items-center gap-4">
      <input bind:this={avatarFileInput} type="file" accept="image/jpeg,image/png,image/gif" onchange={handleFileChange} class="hidden"/>
      <button onclick={triggerFileUpload} class="px-5 py-2.5 bg-slate-900 dark:bg-slate-100 text-white dark:text-slate-900 font-medium rounded-xl cursor-pointer hover:bg-slate-800 dark:hover:bg-slate-200 shadow-sm">
        Change Photo
      </button>
      <button onclick={removeAvatar} class="px-5 py-2.5 border border-slate-300 dark:border-slate-700 font-medium rounded-xl cursor-pointer hover:bg-slate-50 dark:hover:bg-slate-800">
        Remove
      </button>
      <span class="text-slate-500 dark:text-slate-400">JPG, PNG or GIF. Max 2MB.</span>
    </div>

    <!-- Email Section -->
    <div class="pt-6 border-t border-slate-200 dark:border-slate-800">
      <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 p-4 bg-slate-50 dark:bg-slate-800/50 border border-slate-200 dark:border-slate-700 rounded-xl">
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 bg-blue-100 dark:bg-blue-900/30 rounded-lg flex items-center justify-center">
            <svg class="w-5 h-5 text-blue-600 dark:text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"/></svg>
          </div>
          <div>
            <p class="font-medium">Email Address</p>
            <p class="text-xs text-slate-500 dark:text-slate-400">emperor.richard@smak2bpk.penabur.sch.id</p>
          </div>
        </div>
        <div class="flex items-center gap-3">
          <span class="inline-flex items-center px-2.5 py-1 bg-green-100 dark:bg-green-900/30 text-green-700 dark:text-green-400 rounded-lg text-xs font-medium">
            <svg class="w-3 h-3 mr-1" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"/></svg>
            Verified
          </span>
          <button onclick={() => showEmailModal = true} class="px-4 py-2 bg-white dark:bg-slate-800 border border-slate-300 dark:border-slate-600 rounded-lg text-sm font-medium cursor-pointer hover:bg-white dark:hover:bg-slate-700">
            Change
          </button>
        </div>
      </div>
    </div>

    <!-- Password Section -->
    <div class="flex flex-col gap-4 pt-6 border-t border-slate-200 dark:border-slate-800">
      <label class="font-medium">Change Password</label>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <input type="password" placeholder="Current password" class="w-full px-4 py-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500"/>
        <input type="password" placeholder="New password" class="w-full px-4 py-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500"/>
      </div>
      <button onclick={handlePasswordUpdate} class="self-start px-5 py-2.5 bg-blue-600 text-white font-medium rounded-xl cursor-pointer hover:bg-blue-700 shadow-sm">
        Update Password
      </button>
    </div>

    <!-- Danger Zone -->
    <div class="pt-6 border-t border-red-300 dark:border-red-800 bg-red-100 dark:bg-red-950/30 rounded-xl p-6">
      <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
        <div>
          <div class="flex items-center gap-2">
            <svg class="w-5 h-5 text-red-700 dark:text-red-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/></svg>
            <h4 class="font-bold text-red-800 dark:text-red-300 text-base">Delete Account</h4>
          </div>
          <p class="text-red-700 dark:text-red-400 text-sm font-medium mt-1">Once you delete your account, there is no going back. Please be certain.</p>
        </div>
        <button onclick={() => showDeleteModal = true} class="px-6 py-3 bg-red-700 dark:bg-red-600 text-white font-semibold rounded-xl cursor-pointer hover:bg-red-800 dark:hover:bg-red-500 shadow-md">
          Delete Account
        </button>
      </div>
    </div>
  </div>
</section>

<!-- Delete Confirmation Modal -->
{#if showDeleteModal}
<div class="fixed inset-0 bg-black/40 backdrop-blur-[2px] flex items-center justify-center z-50 p-4">
  <div class="bg-white dark:bg-slate-900 border-2 border-red-300 dark:border-red-800 rounded-2xl p-8 max-w-lg w-full shadow-2xl">
    <div class="flex items-center gap-4 mb-4">
      <div class="w-14 h-14 bg-red-100 dark:bg-red-900/40 border-2 border-red-200 dark:border-red-800 rounded-full flex items-center justify-center">
        <svg class="w-7 h-7 text-red-700 dark:text-red-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/></svg>
      </div>
      <div>
        <h3 class="text-xl font-bold text-red-800 dark:text-red-300">Delete Your Account?</h3>
        <p class="text-red-600 dark:text-red-400 text-sm font-medium">This action is permanent and irreversible</p>
      </div>
    </div>
    <p class="text-slate-700 dark:text-slate-300 mb-6 leading-relaxed">
      All your data, including your profile, classes, and grades will be permanently deleted. You will not be able to recover this information.
    </p>
    <div class="flex gap-3 justify-end">
      <button onclick={() => showDeleteModal = false} class="px-5 py-2.5 border border-slate-300 dark:border-slate-700 rounded-xl font-medium cursor-pointer hover:bg-slate-50 dark:hover:bg-slate-800">
        Cancel
      </button>
      <button onclick={confirmDelete} class="px-5 py-2.5 bg-red-700 dark:bg-red-600 text-white font-semibold rounded-xl cursor-pointer hover:bg-red-800 dark:hover:bg-red-500 shadow-md">
        Yes, Delete My Account
      </button>
    </div>
  </div>
</div>
{/if}

<!-- Change Email Modal -->
{#if showEmailModal}
<div class="fixed inset-0 bg-black/40 backdrop-blur-[2px] flex items-center justify-center z-50 p-4">
  <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl p-6 max-w-md w-full shadow-2xl">
    <div class="flex items-center gap-3 mb-4">
      <div class="w-10 h-10 bg-blue-100 dark:bg-blue-900/30 rounded-full flex items-center justify-center">
        <svg class="w-5 h-5 text-blue-600 dark:text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"/></svg>
      </div>
      <h3 class="text-lg font-bold">Change Email Address</h3>
    </div>
    <p class="text-slate-500 dark:text-slate-400 text-sm mb-4">
      For security, please enter your current password and the new email address.
    </p>
    <div class="flex flex-col gap-4 mb-6">
      <div class="flex flex-col gap-2">
        <label class="text-sm font-medium">Current Password</label>
        <input type="password" bind:value={emailPassword} placeholder="Enter your password" class="w-full px-4 py-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500"/>
      </div>
      <div class="flex flex-col gap-2">
        <label class="text-sm font-medium">New Email Address</label>
        <input type="email" bind:value={newEmail} placeholder="new.email@example.com" class="w-full px-4 py-3 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl outline-none focus:ring-2 focus:ring-blue-500"/>
      </div>
    </div>
    <div class="flex gap-3 justify-end">
      <button onclick={() => { showEmailModal = false; emailPassword = ''; newEmail = ''; }} class="px-4 py-2 border border-slate-300 dark:border-slate-700 rounded-xl font-medium cursor-pointer hover:bg-slate-50 dark:hover:bg-slate-800">
        Cancel
      </button>
      <button onclick={handleEmailChange} class="px-4 py-2 bg-blue-600 text-white font-medium rounded-xl cursor-pointer hover:bg-blue-700">
        Change Email
      </button>
    </div>
  </div>
</div>
{/if}

<!-- Email Success Toast -->
{#if showEmailSuccess}
<div class="fixed top-6 right-6 z-50">
  <div class="bg-green-100 dark:bg-green-900/30 border border-green-300 dark:border-green-800 text-green-800 dark:text-green-300 px-6 py-4 rounded-xl shadow-lg flex items-center gap-3">
    <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/></svg>
    <div>
      <p class="font-semibold text-sm">Verification Email Sent</p>
      <p class="text-xs text-green-700 dark:text-green-400">Please check your inbox to confirm the change.</p>
    </div>
  </div>
</div>
{/if}

<!-- Password Success Toast -->
{#if showPasswordSuccess}
<div class="fixed top-6 right-6 z-50">
  <div class="bg-green-100 dark:bg-green-900/30 border border-green-300 dark:border-green-800 text-green-800 dark:text-green-300 px-6 py-4 rounded-xl shadow-lg flex items-center gap-3">
    <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"/></svg>
    <div>
      <p class="font-semibold text-sm">Password Updated</p>
      <p class="text-xs text-green-700 dark:text-green-400">Your password has been changed successfully.</p>
    </div>
  </div>
</div>
{/if}
{/if}