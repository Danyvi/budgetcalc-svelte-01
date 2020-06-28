<script>
  import Title from './Title.svelte';
  let name = '';
  let amount = null;
  // $:console.log({name, amount});
</script>

<section class="form">
  <Title title = "add expense" />
  <form action="" class="expense-form">
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" name="name" id="name" bind:value={name} >
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" name="amount" id="amount" bind:value={amount}>
    </div>
    <p class="form-empty">Please fill out all form fields</p>
    <button type="submit" class="btn btn-block">add expense</button>
    <button type="button" class="close-btn">
      <i class="fas fa-times"></i>
      close
    </button>
  </form>
</section>