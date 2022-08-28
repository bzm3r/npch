<script>
    import IconText from './IconText.svelte';

    export let primaries;
    export let totals;
</script>

<div class="container">
    {#each primaries as primary}
        <td>
            <IconText icon={primary} text={totals[primary]}></IconText>
        </td>
    {/each}
</div>

<style>
    .container {
        display: grid;
        grid-template-columns: repeat(4, 75px);
        grid-template-rows: 75px;
    }
</style>
