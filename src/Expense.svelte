<!-- <script>
  // accessing props
  export let expense;
  console.log(expense);
  
</script>

<div>
  <h2>Title: {expense.name}</h2>
  <h2>Amount: {expense.amount}</h2>
</div> -->

<!-- <script>
  // accessing props
  export let expense;
  let {name, amount, id} = expense; // destructuring
  
</script>

<div>
  <h2>Title: {name}</h2>
  <h2>Amount: {amount}</h2>
</div> -->


<script>
  import { getContext, createEventDispatcher } from 'svelte';
  // accessing props
  export let id;
  export let name = "";
  export let amount = 0;
  // export let removeExpense;

  let displayAmount = false;
  function toggleAmount() {
    displayAmount = !displayAmount;
  }

  const remove = getContext('state');

  const dispatch = createEventDispatcher();
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name} 
      <button class="amount-btn" on:click={toggleAmount}>
        <i class="fas fa-caret-down"></i>
      </button>
    </h2>
    {#if displayAmount}
      <h4>Amount: ${amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn">
      <i class="fas fa-pen"></i>
    </button>
    <!-- <button class="expense-btn delete-btn" on:click="{ () => remove(id) }">
      <i class="fas fa-trash"></i>
    </button> -->
    <button class="expense-btn delete-btn" on:click="{ () => dispatch('delete', {id, name:'hello from expense component'}) }">
      <i class="fas fa-trash"></i>
    </button>
  </div>
</article>