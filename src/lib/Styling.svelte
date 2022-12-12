<script>
    import { check_outros } from "svelte/internal";

    const colors = ["red", "green", "blue"];
</script>

{#each colors as color}
    <label for={color} class:red={color=="red"}>
        {color}
        <input type="checkbox" id={color} value={color} />
    </label>
{/each}

<style>
    .red {
        color: red;
    }
</style>
