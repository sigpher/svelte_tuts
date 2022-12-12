<script>
    const ducks = ["Huey", "Dewey", "Louie"];
    let selectedDucks = new Set();

    const onCheckDuck = (event) => {
        if (event.target.checked) {
            selectedDucks.add(event.target.value);
        } else {
            selectedDucks.delete(event.target.value);
        }
        selectedDucks = selectedDucks;
    };

    const onSelectAll = (event) => {
        if (event.target.checked) {
            selectedDucks = new Set(ducks);
        } else {
            selectedDucks.clear();
        }
        selectedDucks = selectedDucks;
    };
</script>

<ol>
    <li>
        <input
            type="checkbox"
            id="select-all"
            checked={selectedDucks.size === ducks.length}
            on:change={onSelectAll}
        />
        <label for="select-all"><strong>Select all</strong></label>
    </li>
    {#each ducks as duck}
        <li>
            <input
                type="checkbox"
                id={duck}
                value={duck}
                checked={selectedDucks.has(duck)}
                on:change={onCheckDuck}
            />
            <label for={duck}>{duck}</label>
        </li>
    {/each}
</ol>

<p>{selectedDucks.size} ducks selected.</p>

<style>
    ol {
        list-style-type: none;
        padding-left: 0;
    }
</style>
