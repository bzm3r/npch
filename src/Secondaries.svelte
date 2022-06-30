<script>
    import { physicals, socials, knowledges, practicals } from './CharacterData.svelte';
    import SecondariesTable from './SecondariesTable.svelte';
    export let totals;
</script>

<div class="container">
    <div class="physicals">
        <SecondariesTable labels={physicals} {totals}></SecondariesTable>
    </div>
    <div class="socials">
        <SecondariesTable labels={socials} {totals}></SecondariesTable>
    </div>
    <div class="knowledges">
        <SecondariesTable labels={knowledges} {totals}></SecondariesTable>
    </div>
    <div class="practicals">
        <SecondariesTable labels={practicals} {totals}></SecondariesTable>
    </div>
</div>

<style>
    .container {
        display: grid;
        grid-template-columns: max-content max-content;
        grid-template-rows: max-content max-content;
        column-gap: 10px;
        row-gap: 10px;
    }
    .physicals {
        justify-self: center;
    }
    .socials {
        justify-self: center;
    }
    .knowledges {
        justify-self: center;
    }
    .practicals {
        justify-self: center;
    }
</style>