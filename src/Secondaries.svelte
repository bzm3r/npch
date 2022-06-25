<script>
    import { physicals, socials, knowledges, practicals } from './CharacterData.svelte';
    import SecondariesTable from './SecondariesTable.svelte';
    export let totals;
</script>

<table>
    <tr>
        <td>
            <SecondariesTable labels={physicals} {totals}></SecondariesTable>
        </td>
        <td>
            <SecondariesTable labels={socials} {totals}></SecondariesTable>
        </td>
    </tr>
    <tr>
        <td>
            <SecondariesTable labels={knowledges} {totals}></SecondariesTable>
        </td>
        <td>
            <SecondariesTable labels={practicals} {totals}></SecondariesTable>
        </td>
    </tr>
</table>
