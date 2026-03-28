<script lang="ts">
	import { goto } from "$app/navigation";

	function goToLogin() {
		goto("/login");
	}

	import "$lib/style/signin.css";
	import { onMount } from "svelte";
	import Fa from "svelte-fa";
	import { faGoogle } from "@fortawesome/free-brands-svg-icons";
	import { theme } from "$lib/comp/get_theme";
	import { faEye, faEyeSlash } from "@fortawesome/free-solid-svg-icons";
	let isReady = false;

	onMount(async () => {
		theme.set(document.documentElement.getAttribute("data-theme"));
		isReady = true;
	});

	let email = "";
	let username = "";
	let password = "";
	let confirmPassword = "";
	let showPassword = false;
	let showConfirm = false;

	let touched = {
		email: false,
		username: false,
		password: false,
		confirm: false,
	};

	let errors = {
		email: "",
		username: "",
		password: "",
		confirm: "",
	};

	function validateEmail(v: string): boolean {
		return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v);
	}

	function validateUsername(v: string): boolean {
		return /^[a-zA-Z0-9_]{8,}$/.test(v);
	}

	function validatePassword(v: string): boolean {
		return /^(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]).{8,}$/.test(v);
	}

	function validate() {
		errors.email = email && !validateEmail(email) ? "Invalid email." : "";

		errors.username =
			username && !validateUsername(username)
				? "Min 8 char, no space, only _ allowed"
				: "";

		errors.password =
			password && !validatePassword(password)
				? "Must include capital, number, symbol"
				: "";

		errors.confirm =
			confirmPassword && password !== confirmPassword
				? "Password does not match"
				: "";
	}
</script>

<div class="min-h-screen flex bg-gray-900 text-white relative overflow-hidden">
	<!-- LEFT FORM -->
	<div
		class="w-1/2 flex items-center justify-center bg-gray-800/80 backdrop-blur-md p-10 relative z-10 border-r border-white/10"
	>
		<div class="w-full max-w-md">
			<h1 class="text-3xl font-bold mb-6">Sign Up</h1>

			<!-- EMAIL -->
			<label class="label">Enter your email:</label>
			<input
				type="email"
				placeholder="your@example.com"
				bind:value={email}
				on:input={validate}
				on:blur={() => (touched.email = true)}
				class="input {touched.email && errors.email
					? 'border-red-500'
					: ''}"
			/>
			{#if touched.email && errors.email}
				<p class="error">{errors.email}</p>
			{/if}

			<!-- USERNAME -->
			<label class="label">Enter your username:</label>
			<input
				type="text"
				placeholder="Minimum eight characters"
				bind:value={username}
				on:input={validate}
				on:blur={() => (touched.username = true)}
				class="input"
			/>
			{#if touched.username && errors.username}
				<p class="error">{errors.username}</p>
			{/if}
			<!-- PASSWORD -->
			<label class="label">Enter your password:</label>

			<div class="relative">
				<input
					type={showPassword ? "text" : "password"}
					placeholder="Strong Password..."
					bind:value={password}
					on:input={validate}
					on:blur={() => (touched.password = true)}
					class="input pr-10"
				/>
				<button
					type="button"
					class="eye-btn"
					on:click={() => (showPassword = !showPassword)}
				>
					<Fa icon={showPassword ? faEyeSlash : faEye} />
				</button>
			</div>

			{#if touched.password && errors.password}
				<p class="error">{errors.password}</p>
			{/if}
			<!-- CONFIRM -->
			<label class="label">Retype your password:</label>

			<div class="relative">
				<input
					type={showConfirm ? "text" : "password"}
					placeholder="Repeat Your Password"
					bind:value={confirmPassword}
					on:input={validate}
					on:blur={() => (touched.confirm = true)}
					class="input pr-10"
				/>

				<!-- 👁️ ICON -->
				<button
					type="button"
					class="eye-btn"
					on:click={() => (showConfirm = !showConfirm)}
				>
					<Fa icon={showConfirm ? faEyeSlash : faEye} />
				</button>
			</div>

			{#if touched.confirm && errors.confirm}
				<p class="error">{errors.confirm}</p>
			{/if}

			<h1 class="mt-4 font-sans">
				Already have account? click login button
			</h1>
			<!-- BUTTONS -->
			<div class="flex gap-4 mt-6">
				<button class="btn-primary">Sign Up</button>
				<button class="btn-secondary" on:click={goToLogin}>
					Login
				</button>
			</div>

			<button
				class="btn-google mt-4 flex items-center justify-center gap-3"
			>
				<Fa icon={faGoogle} />
				<span>Sign Up with Google</span>
			</button>
		</div>
	</div>
	<div
		class="absolute left-1/2 top-0 h-full w-40 pointer-events-none z-20 fade-edge"
	></div>

	<!-- RIGHT VISUAL -->
	<div
		class="w-1/2 relative flex items-center justify-center overflow-hidden bg-right"
	>
		<!-- 🌊 SHAPE LAYER -->
		<div class="shape shape1"></div>
		<div class="shape shape2"></div>
		<div class="shape shape3"></div>

		<!-- CONTENT -->
		<div class="relative text-center px-10 z-10">
			<h2 class="text-4xl font-bold mb-4">CapoLMS</h2>
			<p class="opacity-80">
				Platform pembelajaran modern untuk siswa dan guru. Belajar jadi
				lebih mudah, rapi, dan terorganisir.
			</p>
		</div>
	</div>
</div>
