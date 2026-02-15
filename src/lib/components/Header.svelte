<script>
    import { onMount } from 'svelte';
    import { MoonIcon, SunIcon } from "@lucide/svelte";
    import { Switch } from "@skeletonlabs/skeleton-svelte";


    let isDark = $state(false);

    // On component mount, check saved theme or system preference
    onMount(() => {
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme) {
            isDark = savedTheme === 'dark';
        }else {
            // Detect system preference if no saved theme
            isDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
        }
        console.log(isDark);
    });

    // Add or remove 'dark' class on <html>
    function updateTheme() {
        localStorage.setItem('theme', isDark ? 'dark' : 'light');
        if (isDark) {
            document.documentElement.classList.add('dark');
        } else {
            document.documentElement.classList.remove('dark');
        }
    }
    $effect(() => {
        updateTheme();
    });
</script>

<header class="items-center justify-between">
    <h1 class="text-xl font-bold ml-10"><a href="/">My Website</a></h1>
    <nav class="btn-group preset-outlined-surface-200-800 flex flex-wrap items-center justify-between">
        <a href="/about"><button>About</button></a>
        <a href="/projects"><button>Projects</button></a>
        <a href="/contact"><button>Contact</button></a>
    </nav>
    <div class="mr-26">
        <Switch checked={!isDark} onCheckedChange={() => isDark = !isDark} >
            <Switch.Control>
                <Switch.Thumb>
                    <Switch.Context>
                        {#snippet children(switch_)}
                            {#if switch_().checked}
                                <SunIcon class="size-4"/>
                            {:else}
                                <MoonIcon class="size-4"/>
                            {/if}
                        {/snippet}
                    </Switch.Context>
                </Switch.Thumb>
            </Switch.Control>
            <Switch.HiddenInput />
        </Switch>
    </div>

</header>
