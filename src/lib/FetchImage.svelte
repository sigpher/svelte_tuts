<script>
    import { onMount } from "svelte";
    import { Picture  } from "svelte-lazy-loader";
    // let photos = [];
    const getPhotos = async () => {
        const res = await fetch("https://jsonplaceholder.typicode.com/photos");
        const data = await res.json();

        if (res.ok) {
            return data;
        } else {
            throw new Error(data);
        }
    };

    let promise = getPhotos();
    onMount(() => {
        promise = getPhotos();
    });
</script>

{#await promise}
    <p>...Fetching Data From the Server</p>
{:then photos}
    <div class="photos">
        {#each photos as photo}
            <figure>
                <Picture 
                    loading="lazy"
                    src={photo.thumbnailUrl}
                    alt={photo.title}
                />
                <figcaption>{photo.title}</figcaption>
            </figure>
        {/each}
    </div>
{:catch error}
    <p>{error.message}</p>
{/await}

<style>
    .photos {
        width: 100%;
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        grid-gap: 8px;
    }
    figure{
        width: 100%;
        margin: 0;
    }
</style>
