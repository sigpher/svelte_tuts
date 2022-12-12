<script>
    import { createEventDispatcher } from "svelte";
    let text = "what the fxxk?";

    const dispatch = createEventDispatcher();
    const sayHello = () => {
        dispatch("message", {
            text,
        });
    };
    const sayHi = () => {
        alert(text);
    };
</script>

<button on:click={sayHello}>Click to say Hello</button>
<button on:click={sayHi}>Click to say Hi</button>
