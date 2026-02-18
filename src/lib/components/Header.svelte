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

    let active = $state("home");
    const links = ["about", "projects", "contact"];
    $effect(() => {
        updateTheme();
    });
</script>

<header class="items-center justify-between shadows">
    <h1 class="text-xl font-bold ml-10"><a href="/" onclick={() => (active = "home")}>My Website</a></h1>
    <div class="btn-group items-center mr-16">
        {#each links as pageLink (pageLink)}
            <a href="/{pageLink}" class="link-button" class:preset-filled-primary-500={active === pageLink} class:dark:preset-filled-tertiary-200-800={active === pageLink} onclick={() => (active = pageLink)}>{pageLink}</a>
        {/each}
    </div>
    <div class="mr-10">
        <Switch checked={!isDark} onCheckedChange={() => isDark = !isDark} >
            <Switch.Control class="preset-filled-primary-200-800 dark:preset-filled-tertiary-200-800">
                <Switch.Thumb >
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
