<script>
  import Title from './Title.svelte';
  export let name = '';
  export let amount = null;
  export let addExpense;
  export let isEditing;
  export let editExpense;
  export let hideForm;
  // $:console.log({name, amount});
  // Reactiveness
  $:isEmpty = !name || !amount
  function handleSubmit(){
    // console.log(`name: ${name}, amount: ${amount}`);
    if (isEditing) {
      editExpense({name, amount})
    } else {
      addExpense({name,amount});
    }
    name='';
    amount=null;
    
  }
</script>

<section class="form">
  <Title title = "add expense" />
  <form action="" class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" name="name" id="name" bind:value={name} >
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" name="amount" id="amount" bind:value={amount}>
    </div>
    {#if isEmpty}
    <p class="form-empty">Please fill out all form fields</p>
    {/if}
    <button type="submit" class="btn btn-block" class:disabled={isEmpty}>
    {#if isEditing}
      edit expense
    {:else}
      add expense
    {/if}
  </button>
    <button type="button" class="close-btn" on:click={hideForm}>
      <i class="fas fa-times"></i>
      close
    </button>
  </form>
</section>