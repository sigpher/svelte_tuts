<script>
    let colors = ["red", "green", "blue"];
    let selectedColors = new Set();

    const onSelectColor = (event) => {
        if (event.target.checked) {
            selectedColors.add(event.target.value);
        } else {
            selectedColors.delete(event.target.value);
        }
        selectedColors = selectedColors;
    };

    const onSelectAll = (event) => {
        if (event.target.checked) {
            selectedColors = new Set(colors);
        } else {
            selectedColors.clear();
        }
        selectedColors = selectedColors;
    };
</script>

<label>
    <input
        type="checkbox"
        checked={colors.length === selectedColors.size}
        on:change={onSelectAll}
    />SelectAll
</label>
{#each colors as color}
    <label>
        <input
            type="checkbox"
            bind:value={color}
            checked={selectedColors.has(color)}
            on:change={onSelectColor}
        />{color}
    </label>
{/each}

<p>{selectedColors.size} colors selected</p>
