<script lang="ts">
  import { goto } from "$app/navigation";
  import Fa from "svelte-fa";
  import {
    faBook,
    faUsers,
    faChartLine,
  } from "@fortawesome/free-solid-svg-icons";

  function goToLogin() {
    goto("/login");
  }
  import { onMount } from "svelte";

  let darkMode = true;

  onMount(() => {
    const saved = localStorage.getItem("theme");
    darkMode = saved ? saved === "dark" : true;
    updateTheme();
  });

  function toggleTheme() {
    darkMode = !darkMode;
    localStorage.setItem("theme", darkMode ? "dark" : "light");
    updateTheme();
  }

  function updateTheme() {
    if (darkMode) {
      document.documentElement.classList.add("dark");
    } else {
      document.documentElement.classList.remove("dark");
    }
  }
</script>

<div
  class="min-h-screen bg-white text-black dark:bg-gray-900 dark:text-white overflow-hidden relative"
>
  <!-- HERO SECTION -->
  <div
    class="flex flex-col items-center justify-center text-center px-10 py-24 min-h-[80vh"
  >
    <!-- LEFT TEXT -->
     
    <div class="max-w-xl">
      <h1 class="text-5xl font-bold leading-tight mb-6">
        Learning Made <span class="text-blue-500">Simple</span> 🚀
      </h1>
      <p class="text-gray-600 dark:text-gray-400 mb-4">
        CapoLMS is a modern learning platform for students and teachers. Manage
        classes, assignments, and materials more easily and organized..
      </p>

      <div class="flex gap-4 justify-center mt-6">
        <button
          class="px-6 py-3 bg-blue-500 rounded-lg hover:bg-blue-600 transition shadow-lg"
          on:click={goToLogin}
        >
          Get Started
        </button>

        <button
          class="px-6 py-3 border border-gray-500 rounded-lg hover:bg-gray-800 transition"
        >
          Learn More
        </button>
      </div>
    </div>

    <!-- RIGHT VISUAL -->
    <div class="relative mt-10 lg:mt-0">
      <div
        class="w-80 h-80 bg-blue-200/40 dark:bg-blue-500/20 rounded-full blur-3xl absolute"
      ></div>
      <div
        class="w-72 h-72 bg-gray-300/40 dark:bg-purple-500/20 rounded-full blur-3xl absolute left-10 top-10"
      ></div>
    </div>
  </div>

  <!-- FEATURES -->
  <div class="px-10 py-12">
    <h2 class="text-3xl font-bold mb-10 text-center">Why Choose CapoLMS?</h2>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <!-- FEATURE 1 -->
      <div
        class="dark:bg-gray-800 p-6 rounded-xl hover:shadow-xl transition group bg-gray-200"
      >
        <div class="text-blue-400 mb-4">
          <Fa icon={faBook} size="lg" />
        </div>
        <h3 class="text-xl font-semibold mb-2 text-black dark:text-white">
          Easy Learning
        </h3>

        <p class="text-gray-600 dark:text-gray-300">
          Akses materi dan tugas dengan mudah dalam satu platform.
        </p>
      </div>

      <!-- FEATURE 2 -->
      <div
        class="dark:bg-gray-800 p-6 rounded-xl hover:shadow-xl transition group bg-gray-200"
      >
        <div class="text-blue-400 mb-4">
          <Fa icon={faUsers} size="lg" />
        </div>
        <h3 class="text-xl font-semibold mb-2">Collaborative</h3>
        <p class="text-gray-400">
          Interaksi antara siswa dan guru jadi lebih efektif.
        </p>
      </div>

      <!-- FEATURE 3 -->
      <div
        class="dark:bg-gray-800 p-6 rounded-xl hover:shadow-xl transition group bg-gray-200"
      >
        <div class="text-blue-400 mb-4">
          <Fa icon={faChartLine} size="lg" />
        </div>
        <h3 class="text-xl font-semibold mb-2">Track Progress</h3>
        <p class="text-gray-400">
          Pantau perkembangan belajar dengan mudah dan real-time.
        </p>
      </div>
    </div>
  </div>

  <!-- CTA -->
  <div class="text-center py-16">
    <h2 class="text-3xl font-bold mb-4">Start Your Learning Journey Today</h2>
    <p class="text-gray-400 mb-6">
      Gabung sekarang dan rasakan pengalaman belajar yang berbeda.
    </p>

    <button
      class="px-8 py-3 bg-blue-500 rounded-lg hover:bg-blue-600 transition shadow-lg"
      on:click={goToLogin}
    >
      Join Now
    </button>
  </div>
</div>
