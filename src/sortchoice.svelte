<script>
    import Fast from './fast.svelte'
    import Slow from './slow.svelte'
    let slow= false, fast = false;
</script>

{#if fast}
    <Fast />
{:else if slow}
    <Slow />
{:else}
    <button on:click={() => fast = true}>Faster and more accurate to the algorithm's speed</button>
    <button on:click={() => slow = true}>Slower but easier to see what is happening and the differences between each algorithm</button>
{/if}