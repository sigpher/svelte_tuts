<script>
    import ListItem from "./lazy/ListItem.svelte";

    let GetData = async () => {
        const res = await fetch("https://jsonplaceholder.typicode.com/photos");
        let photos_json = await res.json();
        if (res.ok) {
            return photos_json;
        } else {
            throw new Error(photos_json);
        }
    };

    let promise = GetData();
</script>

{#await promise}
    <p>Loading...</p>
{:then photos}
    <div id="container">
        {#each photos as item}
            <figure>
                <img loading="lazy" src={item.url} alt={item.title} />
                <figcaption>{item.title}</figcaption>
            </figure>
        {/each}
    </div>
{:catch error}
    <p>{error.message}</p>
{/await}

<style>
    img {
        width: 200px;
        height: 200px;
        display: block;
    }
    #container {
        display: grid;
        width: 400px;
        height: 400px;
        grid-template-columns: repeat(5,1fr);
        grid-gap: 8px;
    }
</style>
