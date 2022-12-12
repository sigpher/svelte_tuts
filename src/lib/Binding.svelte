<script>
    let colors = ["red", "green", "blue"];
    let selectedColor;
</script>

<select name="" id="" bind:value={selectedColor}>
    {#each colors as color}
        <option value={color}>{color}</option>
    {/each}
</select>

<p>{selectedColor}</p>