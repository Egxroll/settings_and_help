<script>
	import Navbar from "$lib/comp/navbar.svelte";
	import Menubar from "$lib/comp/menubar.svelte";
	import { FaSearch } from "svelte-icons/fa";

	let classes = [
		{
			name: "Matematika XIIA-2026/2027",
			subject: "Mathematics",
			teacher: "Darrell, SE.",
			level: "12th Grade",
		},
		{
			name: "IPA",
			subject: "Science",
			teacher: "Dummy",
			level: "Dummy",
			image: "pattern.jpg",
		},
		{
			name: "Bahasa Inggris",
			subject: "English",
			teacher: "Dummy",
			level: "Dummy",
			image: "pattern.jpg",
		},
	];
</script>

<div class="p-6 relative z-10">
	<div class="fixed inset-0 z-0 pointer-events-none">
		<div class="stars-layer"></div>
		<div class="stars"></div>
		<div class="stars2"></div>
		<div class="stars3"></div>
	</div>
	<!-- Header -->
	<div class="mb-8">
		<h2 class="text-3xl font-bold mb-4">Your Dashboard</h2>
		<!-- FILTER + SEARCH (UI ONLY SY BLM BUAT FUNGSI) -->
		<div class="flex flex-col md:flex-row gap-4 mb-6">
			<!-- Dropdown -->
			<select
				class="w-100 px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
			>
				<option>Sort By</option>
				<option>Name (A-Z)</option>
				<option>Name (Z-A)</option>
				<option>Teacher Name (A-Z)</option>
				<option>Teacher Name (Z-A)</option>
				<option>Enrollment Date (Ascending)</option>
				<option>Enrollment Date (Descending)</option>
				<option>Latest Updated</option>
			</select>
			<div class="relative flex-1">
				<input
					type="text"
					placeholder="Search here..."
					class="w-full px-4 py-2 pr-10 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
				/>
				<div
					class="absolute inset-y-0 right-3 flex items-center text-gray-400"
				>
					<div class="w-4 h-4">
						<FaSearch />
					</div>
				</div>
			</div>
		</div>
		<p class="text-gray-500 mt-1 dark:text-white">Welcome back, dummy</p>
	</div>

	<!-- Grid -->
	<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
		{#each classes as cls}
			<div
				class="group relative rounded-xl overflow-hidden border bg-white shadow-sm hover:shadow-2xl transition duration-500 cursor-pointer transform hover:-translate-y2 hover:scale-[1.02]"
			>
				<!-- HEADER -->
				<div
					class="relative h-32 bg-slate-700 text-white overflow-hidden"
				>
					<div
						class="absolute inset-0 opacity-0 group-hover:opacity-100 transition duration-500 bg-blue-500/10 blur-xl"
					></div>

					<!-- Content -->
					<div class="relative z-10 p-4">
						<h2
							class="text-lg font-semibold tracking-wide group-hover:tracking-wider transition"
						>
							{cls.name}
						</h2>

						<p class="text-sm opacity-90">
							{cls.subject}
						</p>

						<p class="text-xs mt-1 opacity-80">
							{cls.teacher}
						</p>

						<p class="text-xs opacity-80">
							{cls.level}
						</p>
					</div>
				</div>

				<!-- FOOTER -->
				<div class="p-4 flex justify-between items-center">
					<span
						class="text-sm text-gray-500 group-hover:text-blue-500 transition"
					>
						Open Class
					</span>

					<button
						class="px-4 py-1.5 text-sm bg-blue-500 text-white rounded-lg
					hover:bg-blue-600 active:scale-90 transition duration-200 shadow-md hover:shadow-lg"
					>
						Enter
					</button>
				</div>

			
				<div
					class="absolute inset-0 rounded-xl border-2 border-transparent group-hover:border-blue-400 transition duration-500"
				></div>
			</div>
		{/each}
	</div>
</div>

<style>
	.stars-layer {
		position: absolute;
		width: 100%;
		height: 100%;
		background-image: radial-gradient(
				2px 2px at 20px 30px,
				white,
				transparent
			),
			radial-gradient(2px 2px at 100px 150px, white, transparent),
			radial-gradient(2px 2px at 200px 80px, white, transparent),
			radial-gradient(2px 2px at 300px 200px, white, transparent),
			radial-gradient(2px 2px at 400px 100px, white, transparent),
			radial-gradient(2px 2px at 500px 250px, white, transparent);
		background-repeat: repeat;
		background-size: 600px 600px;
		animation: twinkle 5s ease-in-out infinite alternate;
	}
	@keyframes twinkle {
		0% {
			opacity: 0.3;
		}
		100% {
			opacity: 0.8;
		}
	}
	.dark .stars-layer {
		filter: brightness(1.5);
	}

	.stars-layer {
		filter: brightness(0.9);
	}
</style>
