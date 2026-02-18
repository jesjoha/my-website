<script>
    import { ChevronDownIcon, GithubIcon } from "@lucide/svelte";
    import { Accordion } from "@skeletonlabs/skeleton-svelte";
    import { slide } from "svelte/transition";

    const projects = [
        {
            id: 1,
            title: "Project 1",
            description: "This project is used to create a project",

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
<p class="m-10">This is what I do/have done. How about that?</p>

<Accordion collapsible>
    {#each projects as project, i (project)}
        {#if i !== 0}
            <hr class="hr" />
        {/if}
        <Accordion.Item value={project.id}>
            <h4>
                <Accordion.ItemTrigger class="font-bold flex items-center justify-between gap-2 border-0 rounded-2xl hover:preset-filled-surface-500">
                    {project.title}
                    <Accordion.ItemIndicator class="group">
                        <ChevronDownIcon class="h-5 w-5 transition group-data-[state=open]:rotate-180" />
                    </Accordion.ItemIndicator>
                </Accordion.ItemTrigger>
            </h4>
            <Accordion.ItemContent>
                {#snippet element(attributes)}
                    {#if !attributes.hidden}
                        <div {...attributes} transition:slide={{ duration: 150 }} class="card border-2 p-10 rounded-2xl">
                            {project.description}
                            <footer class="flex flex-row justify-between">
                                Author: Me
                                {#if project.link}
                                    <a href={project.link} target="_blank" rel="noopener noreferrer">
                                        <button>
                                            <GithubIcon />
                                        </button>
                                    </a>
                                {/if}
                            </footer>
                        </div>
                    {/if}
                {/snippet}
            </Accordion.ItemContent>
        </Accordion.Item>
    {/each}
</Accordion>