<script>
  import { onMount } from 'svelte';
  import { browser } from '$app/environment';

  let currentHash = $state('#profile');

  function updateHash() {
    if (browser) currentHash = window.location.hash || '#profile';
  }

  onMount(() => {
    updateHash();
    window.addEventListener('hashchange', updateHash);
    return () => window.removeEventListener('hashchange', updateHash);
  });

  function setHash(hash) {
    if (browser) window.location.hash = hash;
  }

  const navItems = [
    { hash: '#profile', label: 'Profile & Account', icon: 'M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z' },
    { hash: '#preferences', label: 'App Preferences', icon: 'M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z M15 12a3 3 0 11-6 0 3 3 0 016 0z' },
    { hash: '#notifications', label: 'Notifications', icon: 'M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9' },
    { hash: '#accessibility', label: 'Accessibility', icon: 'M15 12a3 3 0 11-6 0 3 3 0 016 0z M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z' },
  ];
</script>

<aside class="w-72 flex-shrink-0 text-slate-900 dark:text-slate-100">
  <nav class="space-y-2 sticky top-8">
    {#each navItems as item}
      <button 
        onclick={() => setHash(item.hash)}
        class="w-full flex items-center gap-3 px-5 py-4 text-base font-medium rounded-xl transition-all text-left border
          {currentHash === item.hash 
            ? 'bg-white dark:bg-slate-900 shadow-sm border-slate-200 dark:border-slate-800' 
            : 'text-slate-500 dark:text-slate-400 hover:bg-white/80 dark:hover:bg-slate-900/80 hover:shadow-sm border-transparent'}"
      >
        <svg class="w-5 h5 {currentHash === item.hash ? 'text-slate-500 dark:text-slate-400' : 'text-slate-400 dark:text-slate-500'}" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d={item.icon}/>
        </svg>
        {item.label}
      </button>
    {/each}
  </nav>
</aside>