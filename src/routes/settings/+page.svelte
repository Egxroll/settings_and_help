<script>
  import SettingsNav from './sections/SettingsNav.svelte';
  import ProfileSection from './sections/ProfileSection.svelte';
  import PreferencesSection from './sections/PreferencesSection.svelte';
  import NotificationsSection from './sections/NotificationsSection.svelte';
  import AccessibilitySection from './sections/AccessibilitySection.svelte';
</script>

<div class="min-h-screen bg-slate-50 dark:bg-slate-950 text-sm text-slate-900 dark:text-slate-100">
  <div class="max-w-7xl mx-auto px-6 py-8 flex gap-6">
    <SettingsNav />
    <main class="flex-1 flex flex-col gap-6">
      <ProfileSection />
      <PreferencesSection />
      <NotificationsSection />
      <AccessibilitySection />
    </main>
  </div>
</div>