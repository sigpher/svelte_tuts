<script>
    export let item;
    export let lazy = false;
    let src = item;
    let observer = null;

    if (lazy) {
        src = "";
        observer = new IntersectionObserver(onIntersect, {
            rootMargin: "200px",
        });
    }

    function onIntersect(entries) {
        if (!src && entries[0].isIntersecting) {
            src = item;
        }
    }

    function lazyLoad(node) {
        observer && observer.observe(node);
        return {
            destroy() {
                observer && observer.unobserve(node);
            },
        };
    }
</script>

<article use:lazyLoad>
    <img {src} alt="kitten" />
</article>

<style>
    article {
        width: 300px;
        height: 500px;
        margin-bottom: 0.5rem;
    }
</style>
