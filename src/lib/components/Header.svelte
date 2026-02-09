<script>
    import { onMount } from 'svelte';

    import lightmode from '$lib/assets/lightmode.svg'

    let isDark = false;

    // On component mount, check saved theme or system preference
    onMount(() => {
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme) {
            isDark = savedTheme === 'dark';
        }else {
            // Detect system preference if no saved theme
            isDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
        }
        updateTheme();
    });

    // Toggle dark mode and update theme class & localStorage
    function toggleDarkMode() {
        isDark = !isDark;
        updateTheme();
        localStorage.setItem('theme', isDark ? 'dark' : 'light');
    }

    // Add or remove 'dark' class on <html>
    function updateTheme() {
        if (isDark) {
            document.documentElement.classList.add('dark');
        } else {
            document.documentElement.classList.remove('dark');
        }
    }
</script>

<header>
    <h1 class="text-xl font-bold"><a href="/">My Website</a></h1>
    <div class="flex flex-wrap items-center justify-between">
        <button><a href="/about">About</a></button>
        <button>Projects</button>
        <button>Contact</button>
    </div>
    <button class="border-indigo-950 dark:border-gray-500 bg-gray-800 dark:bg-white text-white dark:text-black"
            on:click={toggleDarkMode}
            aria-label="Toggle Dark Mode"
    >
        {#if isDark}
            <!-- Sun icon for light mode -->
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                <path fill="currentColor" d="M17 12a5 5 0 1 1-10 0a5 5 0 0 1 10 0"/><path fill="currentColor" fill-rule="evenodd" d="M12 1.25a.75.75 0 0 1 .75.75v2a.75.75 0 0 1-1.5 0V2a.75.75 0 0 1 .75-.75M1.25 12a.75.75 0 0 1 .75-.75h2a.75.75 0 0 1 0 1.5H2a.75.75 0 0 1-.75-.75m18 0a.75.75 0 0 1 .75-.75h2a.75.75 0 0 1 0 1.5h-2a.75.75 0 0 1-.75-.75M12 19.25a.75.75 0 0 1 .75.75v2a.75.75 0 0 1-1.5 0v-2a.75.75 0 0 1 .75-.75" clip-rule="evenodd"/><path fill="currentColor" d="M3.67 3.716a.75.75 0 0 1 1.059-.048L6.95 5.7a.75.75 0 0 1-1.012 1.107L3.717 4.775a.75.75 0 0 1-.048-1.06m16.663.001a.75.75 0 0 1-.047 1.06l-2.223 2.03A.75.75 0 1 1 17.05 5.7l2.222-2.032a.75.75 0 0 1 1.06.048m-3.306 13.309a.75.75 0 0 1 1.06 0l2.223 2.222a.75.75 0 1 1-1.061 1.06l-2.222-2.222a.75.75 0 0 1 0-1.06m-10.051 0a.75.75 0 0 1 0 1.06l-2.222 2.223a.75.75 0 0 1-1.06-1.06l2.222-2.223a.75.75 0 0 1 1.06 0" opacity="0.5"/>
            </svg>
        {:else}
            <!-- Moon icon for dark mode -->
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                <path fill="currentColor" d="M12 22c5.523 0 10-4.477 10-10c0-.463-.694-.54-.933-.143a6.5 6.5 0 1 1-8.924-8.924C12.54 2.693 12.463 2 12 2C6.477 2 2 6.477 2 12s4.477 10 10 10"/>
            </svg>
        {/if}
    </button>
</header>
