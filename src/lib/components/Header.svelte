<script>
    import { onMount } from 'svelte';

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
    <h1 class="text-xl font-bold">My Website</h1>
    <div class="flex flex-wrap items-center justify-between">
        <button>one</button>
        <button>two</button>
        <button>three</button>
    </div>
    <button
            on:click={toggleDarkMode}
            aria-label="Toggle Dark Mode"
    >
        {#if isDark}
            <!-- Sun icon for light mode -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m8.66-9h-1M4.34 12h-1m12.02 5.66l-.7-.7M7.34 7.34l-.7-.7m12.02 12.02l-.7-.7M7.34 16.66l-.7-.7M12 7a5 5 0 100 10 5 5 0 000-10z" />
            </svg>
        {:else}
            <!-- Moon icon for dark mode -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12.79A9 9 0 1111.21 3 7 7 0 0021 12.79z" />
            </svg>
        {/if}
    </button>
</header>
