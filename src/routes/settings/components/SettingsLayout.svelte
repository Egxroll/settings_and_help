<script>
  import SettingsNav from './SettingsNav.svelte';
  import ProfileSection from './sections/ProfileSection.svelte';
  import PreferencesSection from './sections/PreferencesSection.svelte';
  import NotificationsSection from './sections/NotificationsSection.svelte';
  import PrivacySection from './sections/PrivacySection.svelte';
  import AccessibilitySection from './sections/AccessibilitySection.svelte';
  import ConnectedSection from './sections/ConnectedSection.svelte';
</script>

<div class="min-h-screen bg-gradient-to-br from-[#e0f7fa] via-[#f5f5f5] to-[#fff8e1]">
  <div class="max-w-7xl mx-auto px-6 py-8 flex gap-6">
    <SettingsNav />
    <main class="flex-1">
      <ProfileSection />
      <PreferencesSection />
      <NotificationsSection />
      <PrivacySection />
      <AccessibilitySection />
      <ConnectedSection />
    </main>
  </div>
</div>