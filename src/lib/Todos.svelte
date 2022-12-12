<script>
    import { fly } from "svelte/transition";
    let todos = [
        { done: false, text: "finish Svelte tutorial" },
        { done: false, text: "build an app" },
        { done: false, text: "world domination" },
    ];
    // let selected = [];
    $: selected = todos.filter((t) => t.done);
    $: remainding = todos.filter((t) => !t.done && t.text).length;
    const add = () => {
        todos = todos.concat({ done: false, text: "" });
    };
    const clear = () => {
        todos = todos.filter((t) => !t.done);
    };

    const onSelectAll = (event) => {
        if (event.target.checked) {
            todos.forEach((t) => (t.done = true));
        } else {
            todos.forEach((t) => (t.done = false));
        }
        todos = todos;
    };
</script>

<div id="container">
    <h1>Todos:</h1>
    <button on:click={add}>Add New</button>
    <button on:click={clear}>Clear</button>
    <label for="">
        <span>Select All</span>
        <input
            type="checkbox"
            checked={selected.length === todos.length && todos.length != 0}
            on:change={onSelectAll}
        />
    </label>
    <br />
    {#each todos as todo}
        <input
            type="checkbox"
            bind:checked={todo.done}
            transition:fly={{ x: 200, duration: 300 }}
        />
        <input
            transition:fly={{ x: 200, duration: 300 }}
            type="text"
            bind:value={todo.text}
            placeholder="What's need to be done"
        />
        <br />
    {/each}

    <ol style="text-align: left;">
        {#each selected as item}
            {#if item.text}
                <li>{item.text}</li>
            {/if}
        {/each}
    </ol>
    <p>{remainding} remaindings</p>
</div>

<style>
    input[type="text"] {
        font-size: 0.8em;
        margin: 2px 0;
        border-radius: 3px;
        border-width: 1px;
        padding: 8px;
        font-family: "Cascadia Code";
        width: 300px;
        /* color:#ff3e00; */
        /* background-color: #00c2ff; */
        outline: none;
    }

    input[type="text"]:hover {
        box-shadow: 2px 3px 2px gray;
    }

    /* input[type="checkbox"] {
        cursor: pointer;
        height: 16px;
        width: 16px;
    }
    input[type="checkbox"]:hover {
        box-shadow: 2px 3px 2px gray;
    }
    input[type="check"]:checked::after {
        content: "✓";
        color: #fff;
        font-size: 12px;
        font-weight: bold;
        background: #ff366f;
    } */
    button {
        margin: 5px 5px;
        font-family: "Cascadia Code";

        padding: 8px 4px;
    }
    button:hover {
        box-shadow: 2px 3px 2px gray;
    }
    span {
        font-family: "Cascadia Code";
        font-size: 0.8em;
    }

    input[type="checkbox"] {
        margin-right: 5px;
        cursor: pointer;
        font-size: 14px;
        width: 16px;
        height: 14px;
        position: relative;
    }
    input[type="checkbox"]:after {
        position: absolute;
        width: 15px;
        height: 18px;
        top: 0;
        content: " ";
        color: #fff;
        display: inline-block;
        visibility: visible;
        padding: 0px 2px;
        background: #ffffff;
        border: 1px solid #dddddd;
    }
    input[type="checkbox"]:checked:after {
        content: "✓";
        font-size: 14px;
        font-weight: 600;
        text-align: center;
        margin: 0 auto;
        background-color: #1773d6;
    }
    #container {
        text-align: center;
    }
</style>
