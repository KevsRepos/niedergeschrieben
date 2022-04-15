<script lang="ts">
import { browser } from '$app/env';
import { onMount, tick } from 'svelte';
import {fly} from 'svelte/transition';

let
onTextarea: boolean = false,
title: string = '',
story: string = '';

onMount(() => {
    story = window.localStorage.story || '';
    title = window.localStorage.title || '';
})

$: if(browser) {    
    tick().then(_ => window.localStorage.story = story)
    
    onTextarea = Boolean(story.length); 
}

$: if(browser) {    
    tick().then(_ => window.localStorage.title = title)
}
</script>

<form class="w-3/5 flex flex-col justify-center">
    {#if onTextarea}
    <label for="title" class="text-lg" transition:fly={{y: 150}}>Titel</label>
        <input bind:value={title} id="title" class="mb-2 block z-0 p-3" transition:fly={{y: 150}} required/>
    {/if}
    <label for="story" class="text-lg">Geschichte</label>
    <textarea
        id="story" 
        class="resize-none w-full h-64 p-3 z-10 ppr-background-white" 
        placeholder="Geschichten sind Bedeutungsvoll..." 
        required
        bind:value={story}
    />
    {#if onTextarea}
        <a href="/Story/Share" class="mt-2 z-0 p-3 w-min ppr-border self-center"  transition:fly={{y: -100}}>Teilen...</a>
    {/if}
</form>