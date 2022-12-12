<script>
    const getRandomNumber = async () => {
        const res = await fetch("https://svelte.dev/tutorial/random-number");
        const text = await res.text();

        if (res.ok) {
            return text;
        } else {
            throw new Error(text);
        }
    };

    let promise = getRandomNumber();
    const handleClick = () => {
        promise = getRandomNumber();
    };
</script>

<button on:click={handleClick}>generate random number</button>

<!-- replace this element -->
{#await promise}
    <p>...awaiting</p>
{:then value}
    <p>{value}</p>
{:catch error}
    <p style="color: red">{error.message}</p>
{/await}
