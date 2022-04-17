<script lang="ts">
import { browser } from '$app/env';
import { onMount, tick } from 'svelte';
import {fly} from 'svelte/transition';

export let
title: string,
valid: boolean = false,
doTransition: boolean = false;

let titleMinLength: number = 10;

onMount(() => {
    title = window.localStorage.title || '';
})

$: if(browser) {
    tick().then(_ => window.localStorage.title = title)
}

$: valid = title.length >= titleMinLength;
</script>

<div class="flex flex-col" transition:fly={doTransition && {y: 150}}>
    <label for="title" class="text-lg">Titel</label>
    <input 
        bind:value={title} 
        id="title"
        class:ppr-border-warning={title.length > 0 && title.length < titleMinLength}
        class="block z-0 p-3 w-full" 
        required 
    />
    <span class="mb-2 text-right">{title.length} / {titleMinLength} Zeichen min.</span>
</div>