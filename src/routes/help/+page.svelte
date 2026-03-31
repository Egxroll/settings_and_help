<script>
  import { slide } from 'svelte/transition';
  
  let openCard = $state(null);
  let openItem = $state(null);

  const topics = [
    {
      id: 'faq',
      title: '❓ Frequently Asked Questions',
      items: [
        { q: 'How do I submit an assignment?', a: 'Go to your class page, click the assignment, and hit "Submit". You can upload files or type your answer directly.' },
        { q: 'Where can I see my grades?', a: 'You can see your grades by clicking on the corresponding assignment in your class page.' },
        { q: 'How do I reset my password?', a: 'Go to Settings → Profile & Account. Enter your current password, then your new password twice.' },
        { q: 'Can I change my email address?', a: "Yes, in Settings → Profile. You'll need to verify the new email before it becomes active." }
      ]
    },
    {
      id: 'quickstart',
      title: '🚀 Quick Start Guide',
      items: [
        { q: 'Step 1: Set up your profile', a: 'Go to Settings → Profile. Add your photo, bio, and confirm your email.' },
        { q: 'Step 2: Submit an assignment', a: 'Find your assignment, click "Submit Work", upload your file, and click "Turn In".' },
        { q: 'Step 3: Check your grades', a: 'Visit your assignments to see feedback and scores from your teachers.' },
        { q: 'Step 4: Enabling Notifications', a: 'Enabling notifications will keep you updated on new assignments, materials, and announcements.' }
      ]
    },
    {
      id: 'aboutus',
      title: '👀 About Us',
      items: [
        { q: 'Who are we?', a: 'We are a group of students who are tasked with making a website for our Capolavoro Project. Our team consists of Anoki, Darrell, Nicholas, and Raymond.' },
        { q: "What's new!", a: ['Added settings page.', 'Added help page.', 'Removed Herobrine.'] },
        { q: 'Our Mission', a: 'Make a website for our Capolavoro Project that is user-friendly, informative, and visually appealing.' },
        { q: 'Contact the Team', a: 'Reach out to us at support@capolms.edu for any project inquiries or collaboration ideas.' }
      ]
    }
  ];

  function toggleCard(id) {
    if (openCard === id) {
      openCard = null;
      openItem = null;
    } else {
      openCard = id;
      openItem = null;
    }
  }

  function toggleItem(cardId, itemIndex) {
    const key = `${cardId}-${itemIndex}`;
    openItem = openItem === key ? null : key;
  }
</script>

<div class="min-h-screen bg-slate-50 dark:bg-slate-950 text-slate-900 dark:text-slate-100 p-4 md:p-6">
  <div class="max-w-3xl mx-auto space-y-4">
    
    <div class="text-center space-y-2">
      <h1 class="text-3xl md:text-4xl font-bold">Help Center</h1>
      <p class="text-slate-600 dark:text-slate-400">Find answers or contact support</p>
    </div>

    {#each topics as card}
      <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-xl shadow-sm">
        
        <button 
          onclick={() => toggleCard(card.id)}
          class="w-full px-6 py-5 flex items-center justify-between hover:bg-slate-50 dark:hover:bg-slate-800/50 transition-colors"
        >
          <span class="text-xl font-semibold">{card.title}</span>
          <svg class="w-6 h-6 text-slate-400 transition-transform {openCard === card.id ? 'rotate-180' : ''}" fill="none" viewBox="0 0 24 24">
            <path stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
          </svg>
        </button>

        {#if openCard === card.id}
          <div transition:slide={{ duration: 300 }} class="border-t border-slate-200 dark:border-slate-800 divide-y divide-slate-200 dark:divide-slate-800">
            {#each card.items as item, i}
              {@const key = `${card.id}-${i}`}
              <div>
                <button 
                  onclick={() => toggleItem(card.id, i)}
                  class="w-full px-6 py-4 flex items-center justify-between hover:bg-slate-50 dark:hover:bg-slate-800/50 transition-colors"
                >
                  <span>{item.q}</span>
                  <svg class="w-5 h-5 text-slate-400 transition-transform {openItem === key ? 'rotate-180' : ''}" fill="none" viewBox="0 0 24 24">
                    <path stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
                  </svg>
                </button>

                {#if openItem === key}
                  <div transition:slide={{ duration: 250 }} class="px-6 pb-4 text-slate-600 dark:text-slate-400 text-sm">
                    {#if Array.isArray(item.a)}
                      <ul class="list-disc pl-4 space-y-1">
                        {#each item.a as line}
                          <li>{line}</li>
                        {/each}
                      </ul>
                    {:else}
                      {item.a}
                    {/if}
                  </div>
                {/if}
              </div>
            {/each}
          </div>
        {/if}
      </div>
    {/each}

    <div class="text-center pt-4">
      <div class="inline-flex items-center gap-2 px-6 py-3 bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-full">
        <span class="text-slate-600 dark:text-slate-400">Need help?</span>
        <button onclick={() => {}} class="text-blue-600 dark:text-blue-400 font-medium hover:underline flex items-center gap-1">
          support@capolms.edu
          <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24">
            <path stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" d="M14 5l7 7m0 0l-7 7m7-7H3"/>
          </svg>
        </button>
      </div>
    </div>

  </div>
</div>