<script>
    import ListItem from "./ListItem.svelte";

    const prefix = "https://placekitten.com/g/300/500?image=";
    const items = ["01", "02", "03", "04", "05"].map((num) => prefix + num);
    const hasAPI = "IntersectionObserver" in window;
</script>

{#each items as item, i}
    <ListItem {item} lazy={hasAPI && i > 1} />
{/each}
