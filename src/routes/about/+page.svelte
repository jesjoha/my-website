<script>
    import { Tabs } from '@skeletonlabs/skeleton-svelte';

    const headings = [
        {
            title: 'About',
            paragraphs:
                [
                    'I am studying computer engineering at Åbo Akademi University. I am currently writing my bachelor thesis on the subject of edge computing. ' +
                    'I have a bachelor\'s degree in physiotherapy from Arcada University of Applied Sciences. It might come in handy during my current studies. ' +
                    'Who knows?',
                    'I come from Åland or \'the Åland Islands\', which is a wonderful place! ',
                    'I have a passion for sports, particularly team sports. I have played football for most of my life, and I have the scars to prove it! ',
                    'Technology have always been present in my life and I have always been amazed and curious about how computer works. My grandfather used to bring home ' +
                    'Nokia cell phones, both working and display models, from his job, which I could play with. My first own phone was a Nokia 3310.'
                ],
        },
        {
            title: 'Skills',
            paragraphs:
                [
                    'yes',
                    '(update coming soon)'
                ]
        },
        {
            title: 'Something else',
            paragraphs:
                [
                    'I am the father of two wonderful children. I spend most of my time outside of my studies with them and their mother.',
                ]
        }
    ]
</script>

<h1>Me</h1>

<p class="m-10">This is me. How about that?</p>
<Tabs defaultValue={headings[0].title}>
    <Tabs.List>
        {#each headings as heading}
            <Tabs.Trigger class="flex-1 border-0 hover:preset-filled-surface-500" value={heading.title}>{heading.title}</Tabs.Trigger>
        {/each}
        <Tabs.Indicator />
    </Tabs.List>
    {#each headings as heading}
        <Tabs.Content value={heading.title}>
            {#each heading.paragraphs as paragraph}
                <p class="mt-4">{paragraph}</p>
            {/each}
        </Tabs.Content>
    {/each}
</Tabs>

