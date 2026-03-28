<script>
  // States must be declared BEFORE functions that use them
  let openCard = $state(null);
  let openItem = $state(null);

  const cards = [
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
        { 
          q: 'Who are we?', 
          a: 'We are a group of students who are tasked with making a website for our Capolavoro Project. Our team consists of Anoki, Darrell, Nicholas, and Raymond.' 
        },
        { 
          q: "What's new!", 
          a: [
            'Added settings page.',
            'Added help page.',
            'Removed Herobrine.',
          ]
        },
        { 
          q: 'Our Mission', 
          a: 'Make a website for our Capolavoro Project that is user-friendly, informative, and visually appealing.'
        },
        { 
          q: 'Contact the Team', 
          a: 'Reach out to us at support@capolms.edu for any project inquiries or collaboration ideas.' 
        }
      ]
    }
  ];

  function toggleCard(id) {
    openCard = openCard === id ? null : id;
  }

  function toggleItem(cardId, itemIndex) {
    const key = `${cardId}-${itemIndex}`;
    openItem = openItem === key ? null : key;
  }
</script>

<div class="min-h-screen bg-gradient-to-br from-[#e0f7fa] via-[#f5f5f5] to-[#fff8e1] p-6">
  <div class="max-w-3xl mx-auto">

    <!-- Header -->
    <div class="text-center mb-8 animate-fade-in">
      <h1 class="text-4xl font-bold text-gray-900 mb-2">Help Center</h1>
      <p class="text-gray-600">Find answers or contact support</p>
    </div>

    <!-- Cards -->
    <div class="space-y-4">
      {#each cards as card, cardIndex}
        <div 
          class="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden transition-all duration-300 ease-out hover:shadow-lg hover:-translate-y-0.5"
          style="animation: slide-up 0.5s ease-out {cardIndex * 0.1}s both;"
        >

          <!-- Card Header (Click to open) -->
          <button 
            onclick={() => toggleCard(card.id)}
            class="w-full px-6 py-5 flex items-center justify-between hover:bg-gray-50/80 transition-colors duration-200 group"
          >
            <span class="text-xl font-semibold text-gray-900 group-hover:text-blue-600 transition-colors duration-200">{card.title}</span>
            <div class="w-8 h-8 rounded-full bg-gray-100 flex items-center justify-center group-hover:bg-blue-100 transition-colors duration-200">
              <svg 
                class="w-5 h-5 text-gray-500 transition-transform duration-300 ease-out {openCard === card.id ? 'rotate-180' : ''} group-hover:text-blue-600" 
                fill="none" 
                stroke="currentColor" 
                viewBox="0 0 24 24"
              >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
              </svg>
            </div>
          </button>

          <!-- Card Content (Expandable with animation) -->
          {#if openCard === card.id}
            <div 
              class="border-t border-gray-100 overflow-hidden"
              style="animation: expand 0.4s ease-out;"
            >
              {#each card.items as item, i}
                <div 
                  class="border-b border-gray-100 last:border-0 overflow-hidden"
                  style="animation: slide-in-item 0.35s ease-out {i * 0.08}s both;"
                >
                  <button 
                    onclick={() => toggleItem(card.id, i)}
                    class="w-full px-6 py-4 text-left flex items-center justify-between hover:bg-gray-50/80 transition-all duration-200 group/item"
                  >
                    <span class="font-medium text-gray-800 group-hover/item:text-blue-600 transition-colors duration-200">{item.q}</span>
                    <svg 
                      class="w-4 h-4 text-gray-400 transition-transform duration-200 ease-out {openItem === `${card.id}-${i}` ? 'rotate-180' : ''} group-hover/item:text-blue-500" 
                      fill="none" 
                      stroke="currentColor" 
                      viewBox="0 0 24 24"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
                    </svg>
                  </button>

                  {#if openItem === `${card.id}-${i}`}
                    <div 
                      class="px-6 pb-4 text-gray-600 leading-relaxed"
                      style="animation: fade-slide-down 0.25s ease-out;"
                    >
                      {#if Array.isArray(item.a)}
                        <ul class="list-disc pl-4 space-y-1.5">
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
    </div>

    <!-- Footer with merged contact -->
    <div class="mt-10 text-center">
      <div class="inline-flex items-center gap-2 px-6 py-3 bg-white rounded-full shadow-sm border border-gray-200 hover:shadow-md transition-all duration-300 hover:-translate-y-0.5">
        <span class="text-gray-600">Need help?</span>
        <a href="mailto:support@capolms.edu" class="text-blue-600 font-medium hover:underline flex items-center gap-1">
          support@capolms.edu
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"/>
          </svg>
        </a>
      </div>
    </div>

  </div>
</div>

<style>
  @keyframes slide-up {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes expand {
    from {
      opacity: 0;
      max-height: 0;
    }
    to {
      opacity: 1;
      max-height: 1000px;
    }
  }

  @keyframes fade-slide-down {
    from {
      opacity: 0;
      transform: translateY(-10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes slide-in-item {
    from {
      opacity: 0;
      transform: translateX(-15px);
    }
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  .animate-fade-in {
    animation: slide-up 0.6s ease-out;
  }
</style>