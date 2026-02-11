<script>
    import { ChevronDownIcon, GithubIcon } from "@lucide/svelte";
    import { Accordion } from "@skeletonlabs/skeleton-svelte";
    import { slide } from "svelte/transition";

    const projects = [
        {
            id: 1,
            title: "Project 1",
            description: "This project is used to create a project",
            link: "https://svenska.yle.fi",
        },
        {
            id: 2,
            title: "Project 2",
            description: "This project is used to create a project and this was project nr 2.",
            link: "https://github.com",
        },
        {
            id: 3,
            title: "Project 3",
            description: "This is the final project of the test.",
            link: "https://ecosia.org",
        }
    ];

</script>

<h1>Projects</h1>
<p>This is what I do/have done. How about that?</p>

<Accordion collapsible>
    {#each projects as project, i (project)}
        {#if i !== 0}
            <hr class="hr" />
        {/if}
        <Accordion.Item value={project.id}>
            <h4>
                <Accordion.ItemTrigger class="font-bold flex items-center justify-between gap-2 border-0">
                    {project.title}
                    <Accordion.ItemIndicator class="group">
                        <ChevronDownIcon class="h-5 w-5 transition group-data-[state=open]:rotate-180" />
                    </Accordion.ItemIndicator>
                </Accordion.ItemTrigger>
            </h4>
            <Accordion.ItemContent>
                {#snippet element(attributes)}
                    {#if !attributes.hidden}
                        <div {...attributes} transition:slide={{ duration: 150 }}>
                            {project.description}
                            <footer class="flex flex-row justify-between">
                                <a href={project.link} target="_blank" rel="noopener noreferrer">
                                    <GithubIcon />
                                </a>
                                Author: Me
                            </footer>
                        </div>
                    {/if}
                {/snippet}
            </Accordion.ItemContent>
        </Accordion.Item>
    {/each}
</Accordion>