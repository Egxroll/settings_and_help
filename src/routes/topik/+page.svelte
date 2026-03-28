<script lang="ts">
    import Navbar from "$lib/comp/navbar.svelte";
    import Menubar from "$lib/comp/menubar.svelte";
    import Fa from "svelte-fa";
    import {
        faBook,
        faClipboard,
        faQuestionCircle,
    } from "@fortawesome/free-solid-svg-icons";
    let openIndex: number | null = null;

    let topics = [
        {
            title: "Algebra Basics",
            desc: "Learn about variables and equations",
            material: 5,
        },
        {
            title: "Linear Equations",
            desc: "Solve linear equations step by step",
            material: 8,
        },
        {
            title: "Trigonometry",
            desc: "Introduction to sin, cos, tan",
            material: 6,
        },
    ];

    function toggle(index: number) {
        openIndex = openIndex === index ? null : index;
    }
</script>

<div class="p-6">
    <!-- HEADER -->
    <div class="mb-8">
        <h1 class="text-3xl font-bold">Mathematics XIIA</h1>
        <p class="text-gray-500 dark:text-gray-300">
            List of topics in this class
        </p>
    </div>

    <!-- TOPICS -->
    <div class="space-y-4">
        {#each topics as topic, i}
            <div
                class="bg-gray-200 dark:bg-gray-800 rounded-xl overflow-hidden transition"
            >
                <!-- TOP BAR -->
                <div
                    class="p-5 flex justify-between items-center cursor-pointer"
                    on:click={() => toggle(i)}
                >
                    <div>
                        <h2
                            class="text-lg font-semibold text-black dark:text-white"
                        >
                            {topic.title}
                        </h2>
                        <p class="text-sm text-gray-600 dark:text-gray-300">
                            {topic.desc}
                        </p>
                    </div>

                    <button
                        class="px-4 py-1.5 bg-blue-500 text-white rounded-lg text-sm hover:bg-blue-600 transition"
                    >
                        {openIndex === i ? "Close" : "Open"}
                    </button>
                </div>

                <!-- DROPDOWN -->
                {#if openIndex === i}
                    <div class="px-5 pb-5 space-y-3 animate-slide">
                        <div
                            class="p-3 rounded-lg bg-white dark:bg-gray-700 flex justify-between items-center hover:bg-gray-100 dark:hover:bg-gray-600 transition"
                        >
                            <div class="flex items-center gap-2">
                                <Fa
                                    icon={faBook}
                                    class="text-blue-500 w-4 h-4"
                                />
                                <span>Materi</span>
                            </div>

                            <button
                                class="text-sm text-blue-500 hover:underline"
                            >
                                View
                            </button>
                        </div>

                        <div
                            class="p-3 rounded-lg bg-white dark:bg-gray-700 flex justify-between items-center hover:bg-gray-100 dark:hover:bg-gray-600 transition"
                        >
                            <div class="flex items-center gap-2">
                                <Fa
                                    icon={faClipboard}
                                    class="text-green-500 w-4 h-4"
                                />
                                <span>Tugas</span>
                            </div>

                            <button
                                class="text-sm text-blue-500 hover:underline"
                            >
                                View
                            </button>
                        </div>

                        <div
                            class="p-3 rounded-lg bg-white dark:bg-gray-700 flex justify-between items-center hover:bg-gray-100 dark:hover:bg-gray-600 transition"
                        >
                            <div class="flex items-center gap-2">
                                <Fa
                                    icon={faQuestionCircle}
                                    class="text-purple-500 w-4 h-4"
                                />
                                <span>Kuis</span>
                            </div>

                            <button
                                class="text-sm text-blue-500 hover:underline"
                            >
                                View
                            </button>
                        </div>
                    </div>
                {/if}
            </div>
        {/each}
    </div>
</div>

<style>
    @keyframes slideDown {
        from {
            opacity: 0;
            transform: translateY(-10px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .animate-slide {
        animation: slideDown 0.3s ease;
    }
</style>
