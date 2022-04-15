<script lang="ts">
import '../paper.min.css';
import '../app.css';
import { onMount } from 'svelte';

let clientTheme: string;

onMount(() => {
    clientTheme = window && window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';

    toggleTheme(clientTheme);
});

const toggleTheme = theme => {
    document.querySelector('html').className = "";
    document.querySelector('html').classList.add(theme);
}
</script>


<nav class="ppr-border fixed flex justify-between">
    <a href="/" class="ppr-border-none p-2">Niedergeschrieben.net</a>
    <div>
        <select value={clientTheme} on:change={e => toggleTheme(e.currentTarget.value)}>
            <option value="light">light</option>
            <option value="dark">Dark</option>
        </select>
    </div>
</nav>

<slot />