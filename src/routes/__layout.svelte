<script lang="ts">
import '../paper.min.css';
import '../app.css';

let darkTheme: boolean = false;

const toggleTheme = _ => {

    document.querySelector('html').classList.add('dark');
}
</script>


<nav class="ppr-border fixed flex flex-wrap">
    <a href="/" class="ppr-border-none p-2">Niedergeschrieben.net</a>
    <div>
        <select>
            <option>Dark</option>
            <option>light</option>
        </select>
    </div>
</nav>

<slot />