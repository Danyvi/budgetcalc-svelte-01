<script>
import SectionTitle from './Title.svelte'; 
import Expense from './Expense.svelte';
export let expenses = [];
// export let removeExpense;
</script>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>

<section>
  <SectionTitle title = "Expense List" />
  <ul>
    {#each expenses as expense, index}
       <!-- <Expense expense = {expense}/> -->
       <!-- <Expense {...expense} removeExpense = { removeExpense }/> this destructures the objects in its properties -->
       <Expense {...expense} on:delete/> <!-- this destructures the objects in its properties -->
       {:else}
        <h2>No expenses added to the list</h2>
    {/each}
  </ul>
</section>