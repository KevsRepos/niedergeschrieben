<script lang="ts">
import {fly} from 'svelte/transition';

let onTextarea: boolean = false;

const addInputs = textareaNotEmpty => textareaNotEmpty.length ? true : false;
</script>

<form class="w-3/5 flex flex-col justify-center">
    {#if onTextarea}
    <label for="title" class="text-lg" transition:fly={{y: 100}}>Titel</label>
        <input id="title" class="mb-2 block z-0 p-3" transition:fly={{y: 100}} required/>
    {/if}
    <label for="story" class="text-lg">Geschichte</label>
    <textarea
        id="story" 
        class="resize-none w-full h-64 p-3 z-10 ppr-background-white" 
        placeholder="Geschichten sind Bedeutungsvoll..." 
        on:input={e => onTextarea = addInputs(e.currentTarget.value)}
        required
    />
    {#if onTextarea}
        <button type="submit" class="mt-2 block z-0 p-3"  transition:fly={{y: -50}}>Teilen...</button>
    {/if}
</form>