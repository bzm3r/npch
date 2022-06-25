<script>
    export let totals;
    export let labels = [];
</script>

<table>
    {#each labels as label}
    <tr>
        <th>{label}</th>
        <td>{totals[label]}</td>
    </tr>
    {/each}
</table>

<style>
    tr:nth-of-type(odd) {
    background-color:#ccc;
  }
</style>

