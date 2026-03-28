<div class="p-6 flex gap-6">
    <!-- KIRI: kotak besar untuk mengerjakan tugas -->
    <div
        class="flex-1 bg-gray-100 dark:bg-gray-800 p-6 rounded-xl shadow-lg flex flex-col gap-6"
    >
        <!-- Deskripsi Tugas -->
        <div>
            <h2 class="text-2xl font-bold mb-2 text-gray-800 dark:text-white">
                Tugas Matematika: Persamaan Linear
            </h2>
            <p class="text-gray-700 dark:text-gray-300">
                Kerjakan soal berikut ini dan unggah jawabanmu dalam format PDF
                atau gambar. Pastikan jawaban lengkap dan jelas.
            </p>
        </div>

        <!-- Kolom Jawaban / Upload -->
        <div class="flex flex-col gap-4">
            <label class="text-gray-800 dark:text-gray-200 font-semibold"
                >Tulis Jawaban / Upload File</label
            >
            <textarea
                class="w-full p-3 rounded-lg border focus:outline-none focus:ring-2 focus:ring-blue-400 dark:bg-gray-700 dark:text-white"
                rows="10"
                placeholder="Tulis jawabanmu di sini..."
            ></textarea>

            <input
                type="file"
                class="w-full text-gray-700 dark:text-gray-300"
            />
        </div>

        <!-- Tombol Simpan & Submit -->
        <div class="flex gap-3">
            <button
                class="flex-1 p-4 rounded-xl bg-green-500 hover:bg-green-600 text-white font-bold transition"
            >
                Simpan Jawaban
            </button>
            <button
                class="flex-1 p-4 rounded-xl bg-purple-500 hover:bg-purple-600 text-white font-bold transition"
            >
                Submit Tugas
            </button>
        </div>
    </div>

    <!-- KANAN: kotak lebih kecil untuk deadline & catatan guru -->
    <div class="w-64 flex flex-col gap-6">
        <!-- Deadline -->
        <div class="p-4 bg-white dark:bg-gray-700 rounded-xl shadow">
            <h3 class="font-bold mb-2 text-gray-800 dark:text-white">
                Deadline
            </h3>
            <p class="text-gray-700 dark:text-gray-300">22 Maret 2026, 23:59</p>
        </div>

        <!-- Note dari Guru -->
        <div
            class="p-4 bg-white dark:bg-gray-700 rounded-xl shadow flex flex-col gap-2"
        >
            <h3 class="font-bold mb-2 text-gray-800 dark:text-white">
                Catatan Guru
            </h3>
            <p class="text-gray-700 dark:text-gray-300 text-sm">
                Harap kerjakan soal dengan rapi dan sertakan langkah-langkah
                perhitungan. Jika ada pertanyaan, tanyakan sebelum deadline.
            </p>
        </div>
    </div>
</div>
