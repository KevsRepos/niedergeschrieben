<script lang="ts">
import { browser } from '$app/env';
import { onMount, tick } from 'svelte';

export let
story: string,
valid: boolean = false,
doTransition: boolean = false;

let storyMinLength: number = 10;

onMount(() => {
    story = window.localStorage.story || '';
})

$: if(browser) {
    tick().then(_ => window.localStorage.story = story)
}

$: valid = story.length >= storyMinLength;
</script>

{#if doTransition && story.length}
    <label for="story" class="text-lg">Geschichte</label>
{/if}
<textarea
    id="story"
    class:ppr-border-warning={story.length > 0 && story.length < storyMinLength}
    class="resize-none w-full h-64 p-3 z-10 ppr-background-white" 
    placeholder="Geschichten sind Bedeutungsvoll..." 
    bind:value={story}

    minlength={storyMinLength}
/>
{#if doTransition && story.length}
    <span class="text-right">{story.length} / {storyMinLength} Zeichen min.</span>
{/if}