<script>
    import BoardListItem from "./boardListItem.svelte";
    export let items;

</script>


<div class="list-container">
    <div class="list">
        {#if items.length > 0}
            {#each items as item}
                <BoardListItem item={item} />
            {/each}
        {/if}
    </div>
</div>