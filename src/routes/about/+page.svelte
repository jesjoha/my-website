<script>
    import { Tabs } from '@skeletonlabs/skeleton-svelte';

    const headings = [
        {
            title: 'About',
            text: 'This is the About Page about me.',
        },
        {
            title: 'Hobbies',
            text: 'Hobbies that I enjoy.',
        },
        {
            title: 'Something else',
            text: 'Something else about me. Something else about me. Something else about me. ' +
                'Something else about me. Something else about me. Something else about me. Something else about me. ' +
                'Something else about me. Something else about me. Something else about me. Something else about me. ' +
                'Something else about me. Something else about me. Something else about me. Something else about me. ' +
                'Something else about me. Something else about me. Something else about me. Something else about me. ' +
                'Something else about me. Something else about me. Something else about me. Something else about me. ' +
                'Something else about me. Something else about me. Something else about me. Something else about me. ' +
                'Something else about me. Something else about me. Something else about me. Something else about me. THE END',
        }
    ]
</script>

<h1>Me</h1>

<p class="m-10">This is me. How about that?</p>
<Tabs defaultValue={headings[0].title}>
    <Tabs.List>
        {#each headings as heading}
            <Tabs.Trigger class="flex-1 border-0" value={heading.title}>{heading.title}</Tabs.Trigger>
        {/each}
        <Tabs.Indicator />
    </Tabs.List>
    {#each headings as heading}
        <Tabs.Content value={heading.title}>
            {heading.text}
        </Tabs.Content>
    {/each}
</Tabs>

