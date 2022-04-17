<script lang="ts">
import {fly} from 'svelte/transition';
import { browser } from '$app/env';
import { goto } from '$app/navigation';
import StoryText from '$lib/components/layout/inputs/StoryText.svelte';
import StoryTitle from '$lib/components/layout/inputs/StoryTitle.svelte';

export let
doTransition: boolean = false,
submitText: string;

let
onTextarea: boolean = false,
title: string = '',
story: string = '',
titleValid: boolean = false,
storyValid: boolean = false;

$: if(browser && doTransition) onTextarea = Boolean(story.length);
</script>

<form on:submit|preventDefault={_ => (titleValid && storyValid) && goto('/Story/Tags')} class="flex flex-col justify-center">
    {#if onTextarea || !doTransition}
        <StoryTitle bind:title bind:valid={titleValid} {doTransition} />
    {/if}
        <StoryText bind:story bind:valid={storyValid} {doTransition} />
    {#if onTextarea || !doTransition}
        <button type="submit" class="mt-2 p-3 flex items-center "  transition:fly={{y: -100}}>
            {submitText}
        </button>
    {/if}
</form>