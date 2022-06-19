<script>
    import { physicals, socials, knowledges, practicals } from './CharacterData.svelte';
    import SecondaryTable from './SecondaryTable.svelte';
    export let totals;
</script>

<table>
    <tr>
        <td>
            <SecondaryTable labels={physicals} {totals}></SecondaryTable>
        </td>
        <td>
            <SecondaryTable labels={socials} {totals}></SecondaryTable>
        </td>
    </tr>
    <tr>
        <td>
            <SecondaryTable labels={knowledges} {totals}></SecondaryTable>
        </td>
        <td>
            <SecondaryTable labels={practicals} {totals}></SecondaryTable>
        </td>
    </tr>
</table>
