<script lang="ts">
    import { goto } from "$app/navigation";

    function ayam() {
        goto("/dashboard"); // langsung ke dashboard tanpa validasi
    }

    import "$lib/style/signin.css";
    import { onMount } from "svelte";
    import Fa from "svelte-fa";
    import { faGoogle } from "@fortawesome/free-brands-svg-icons";
    import { faEye, faEyeSlash } from "@fortawesome/free-solid-svg-icons";
    import { theme } from "$lib/comp/get_theme";

    let isReady = false;

    onMount(() => {
        theme.set(document.documentElement.getAttribute("data-theme"));
        isReady = true;
    });

    let email = "";
    let password = "";
    let showPassword = false;

    let touched = {
        email: false,
        password: false,
    };

    let errors = {
        email: "",
        password: "",
    };

    function validateEmail(v: string): boolean {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v);
    }

    function validatePassword(v: string): boolean {
        return v.length >= 6; // simple validation: min 6 chars
    }

    function validate() {
        errors.email = email && !validateEmail(email) ? "Invalid email." : "";
        errors.password =
            password && !validatePassword(password)
                ? "Password must be at least 6 characters"
                : "";
    }

    function login() {
        validate();
        if (!errors.email && !errors.password) {
            console.log("Logging in with:", { email, password });
            // TODO: integrate API login here
        }
    }
</script>

<div class="min-h-screen flex bg-gray-900 text-white relative overflow-hidden">
    <!-- LEFT FORM -->
    <div
        class="w-1/2 flex items-center justify-center bg-gray-800/80 backdrop-blur-md p-10 relative z-10 border-r border-white/10"
    >
        <div class="w-full max-w-md">
            <h1 class="text-3xl font-bold mb-6">Login</h1>

            <!-- EMAIL -->
            <label class="label">Email:</label>
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

            <!-- PASSWORD -->
            <label class="label">Password:</label>
            <div class="relative">
                <input
                    type={showPassword ? "text" : "password"}
                    placeholder="Your password"
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
            <p class="mt-4 ">
                Don’t have an account? click
                <a href="/signup" class="text-blue-500 hover:underline">
                    here mate
                </a>
            </p>
            <!-- BUTTON LOGIN -->
            <button class="btn-primary mt-6 w-full" on:click={ayam}>
                Login
            </button>
            <!-- Optional: Google login -->
            <button
                class="btn-google mt-4 flex items-center justify-center gap-3 w-full"
            >
                <Fa icon={faGoogle} />
                <span>Login with Google</span>
            </button>
        </div>
    </div>

    <!-- RIGHT VISUAL (bisa tetap sama seperti SignUp) -->
    <div class="w-1/2 flex flex-col items-center justify-center">
        <div class="shape shape1"></div>
        <div class="shape shape2"></div>
        <div class="shape shape3"></div>

        <div class="relative text-center px-10 z-10">
            <h2 class="text-4xl font-bold mb-4">CapoLMS</h2>
            <p class="opacity-80">
                Platform pembelajaran modern untuk siswa dan guru. Belajar jadi
                lebih mudah, rapi, dan terorganisir.
            </p>
        </div>
    </div>
</div>
