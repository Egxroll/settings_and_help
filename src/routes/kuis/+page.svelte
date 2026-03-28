<div class="p-6 flex gap-6">
    <!-- KIRI: kotak soal -->
    <div
        class="flex-1 bg-gray-100 dark:bg-gray-800 p-6 rounded-xl shadow-lg max-w-full w-full"
        style="min-height: 200px; max-height: auto;"
    >
        <div>
            <h2 class="text-xl font-bold mb-4 text-gray-800 dark:text-white">
                1. Contoh Pertanyaan Kuis
            </h2>

            <div class="space-y-3">
                <button
                    class="w-full text-left p-3 rounded-lg border hover:bg-blue-100 dark:hover:bg-blue-900 transition bg-white dark:bg-gray-700"
                >
                    A. Pilihan Jawaban A
                </button>
                <button
                    class="w-full text-left p-3 rounded-lg border hover:bg-blue-100 dark:hover:bg-blue-900 transition bg-white dark:bg-gray-700"
                >
                    B. Pilihan Jawaban B
                </button>
                <button
                    class="w-full text-left p-3 rounded-lg border hover:bg-blue-100 dark:hover:bg-blue-900 transition bg-white dark:bg-gray-700"
                >
                    C. Pilihan Jawaban C
                </button>
                <button
                    class="w-full text-left p-3 rounded-lg border hover:bg-blue-100 dark:hover:bg-blue-900 transition bg-white dark:bg-gray-700"
                >
                    D. Pilihan Jawaban D
                </button>

                <!-- Tombol Simpan & Soal Selanjutnya langsung setelah pilihan D -->
                <div class="mt-4 flex gap-3">
                    <button
                        class="flex-1 p-3 rounded-lg bg-green-500 hover:bg-green-600 text-white font-bold transition"
                    >
                        Simpan Jawaban
                    </button>
                    <button
                        class="flex-1 p-3 rounded-lg bg-blue-500 hover:bg-blue-600 text-white font-bold transition"
                    >
                        Soal Selanjutnya
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- KANAN: navigasi soal + submit -->
    <div class="w-64 flex flex-col gap-6">
        <!-- Timer -->
        <div
            class="p-4 bg-white dark:bg-gray-700 rounded-xl shadow text-center"
        >
            <h3 class="font-bold text-lg">Time Left</h3>
            <p class="text-2xl mt-2 font-mono">05:00</p>
        </div>

        <!-- Navigasi soal -->
        <div
            class="p-4 bg-white dark:bg-gray-700 rounded-xl shadow flex flex-col gap-4"
        >
            <h3 class="font-bold mb-3 text-gray-800 dark:text-white">
                Navigasi Soal
            </h3>
            <div class="grid grid-cols-5 gap-3">
                {#each Array(10) as _, i}
                    <button
                        class="p-3 rounded-lg border font-semibold shadow text-center transition
                        bg-gray-200 dark:bg-gray-600 hover:scale-105"
                    >
                        {i + 1}
                    </button>
                {/each}
            </div>

            <!-- Submit Kuis -->
            <button
                class="mt-4 w-full p-4 bg-purple-500 hover:bg-purple-600 text-white font-bold rounded-xl shadow transition"
            >
                Submit Kuis
            </button>
        </div>
    </div>
</div>
    