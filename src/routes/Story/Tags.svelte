<script lang="ts">
import {slide} from 'svelte/transition';
import Center from "$lib/components/layout/Center.svelte";

let
minTags = 2,
maxTags = 6,
tagValues: Array<string> = Array(minTags).fill('');

console.log(tagValues);

const addTags = _ => {
    if(tagValues.length < maxTags) {
        tagValues = [...tagValues, ''];
    }
}

const uploadStory = _ => {

}
</script>

<Center>
    <main class="mb-8">
        <p>
            Setze Tags, welche unseren Filtertieren und Suchhamstern helfen deine Story aufzufinden.
            Was ist es, worum geht es? Schreibst Du von Liebe, Bedauern, Trauer, Glück oder Habgier?<br />
            2 Tags zu setzen ist laut Hamsterrat Pflicht, 4 wären toll und 6 wären echt lieb.
        </p>
    </main>

    {#each tagValues as _, i}
        <label for="tag{i}">Tag {i + 1}</label>
        <input id="tag{i}" class="mb-2" required={i === 0 || i === 1} in:slide/>
    {/each}

    {#if tagValues.length < maxTags}
        <button on:click={addTags} class="mt-4 p-1">Mehr Tags</button>
    {/if}

    <button on:click={uploadStory} class="mt-8 w-full ppr-background-primary text-white p-4">
        Teilen...
    </button>
</Center>