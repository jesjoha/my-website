<script>
    import { ChevronDownIcon, GithubIcon } from "@lucide/svelte";
    import { Accordion } from "@skeletonlabs/skeleton-svelte";
    import { slide } from "svelte/transition";

    const projects = [
        {
            id: 1,
            title: "WorkoutPlanner",
            description: "I have created a new course project for a course on object-oriented software design. The application is a workout planner where the user can plan and perform workouts. " + 
                        "An exercise library is stored in json and the user can add exercises to and remove them from the library in a dedicated tab. Completed workouts are saved and used for statistics. " + 
                        "The project is developed in Java with JavaFX for the GUI. The Jackson-library is used to handle parsing to and from json. The project uses several common design pattern from the course. " + 
                        "Because of the risk of plagiarism and cheating in future course versions, the source code can unfortunately not be shared.",

        },
        {
            id: 2,
            title: "My website",
            description: "You are looking at it right now. My own website to present myself, what I have done and what I can do. It is mostly for practicing my own (frontend) skills but if someone else find something useful from it, that is great!",
            link: "https://github.com/jesjoha/my-website",
        },
        {
            id: 3,
            title: "FoodPlanner (in progress)",
            description: "This a project meant for our family. We sometimes struggle with planning the meals for a week. My wife has been asking for this for some time already so it is time to get this project running! " + 
                          "I'm still not sure if the project name should be FoodPlanner or MealPlanner...",
            link: "https://github.com/jesjoha/FoodPlanner",
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
