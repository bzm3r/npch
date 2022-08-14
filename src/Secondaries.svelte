<script>
    import { physicals, socials, knowledges, practicals } from './CharacterData.svelte';
    import SecondariesTable from './SecondariesTable.svelte';
    import Specials from './Specials.svelte';
    export let totals;
    export let specials;
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
    <div class="specials">
        <Specials {specials}></Specials>
    </div>
</div>



<style>
    .container {
        display: grid;
        grid-template-columns: max-content max-content;
        grid-template-rows: auto;
        grid-template-areas:
        "physicals socials"
        "knowledges practicals"
        "specials specials";
        column-gap: 10px;
        row-gap: 10px;
    }
    .physicals {
        justify-self: center;
        grid-area: physicals;
    }
    .socials {
        justify-self: center;
        grid-area: socials;
    }
    .knowledges {
        justify-self: center;
        grid-area: knowledges;
    }
    .practicals {
        justify-self: center;
        grid-area: practicals;
    }
    .specials {
        justify-self: center;
        grid-area: specials;
    }
</style>