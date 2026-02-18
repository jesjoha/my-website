<script>
    import {MailIcon, GithubIcon, LinkedinIcon, CopyIcon } from "@lucide/svelte";
    import { Popover, Portal, Toast, createToaster } from "@skeletonlabs/skeleton-svelte";

    const toaster = createToaster(
        {
            placement: "top",
        }
    );
    const email = "jesper.johans@proton.me";
    const linkedIn = "https://linkedin.com/in/jesperjohans/";
    const github = "https://github.com/jesjoha";

    const copyToClipboard = async () => {
        try {
            await navigator.clipboard.writeText(email);
            toaster.success({
                description: "Copied to clipboard",
            });
        } catch (error) {
            toaster.error({
                description: error.message,
            });
        }
    };

</script>

<h1>Me</h1>
<p class="m-10">This is my contact info. How about that?</p>
<div class="card items-center justify-between flex p-10 shadows rounded-4xl">
    <Popover>
        <Popover.Trigger>
            <MailIcon/>
        </Popover.Trigger>
        <Portal>
            <Popover.Positioner>
                <Popover.Content class="card rounded-2xl max-w-md p-4 bg-surface-50-950 shadow-xl shadow-primary-300 dark:shadow-tertiary-800">
                    <Popover.Description class="flex items-center">
                        {email}
                        <button class="border-0" on:click={copyToClipboard}>
                            <CopyIcon />
                        </button>
                    </Popover.Description>
                    <Popover.Arrow class="[--arrow-size:--spacing(2)] [--arrow-background:var(--color-surface-50-950)]">
                        <Popover.ArrowTip />
                    </Popover.Arrow>
                </Popover.Content>
            </Popover.Positioner>
        </Portal>
    </Popover>
    <a href={linkedIn} target="_blank" rel="noopener noreferrer"><button><LinkedinIcon /></button></a>
    <a href={github} target="_blank" rel="noopener noreferrer"><button><GithubIcon /></button></a>
</div>
<Toast.Group {toaster}>
    {#snippet children(toast)}
        <Toast {toast} class="preset-tonal-primary dark:preset-tonal-tertiary">
            <Toast.Message>
                <Toast.Description>{toast.description}</Toast.Description>
            </Toast.Message>
        </Toast>
    {/snippet}
</Toast.Group>