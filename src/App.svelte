<script>
	import { setContext } from 'svelte';
	const state = {
		name: 'simple name',
		remove: removeExpense 
	}
	// Components
	import Navbar from './Navbar.svelte';
	import ExpensesList from './ExpensesList.svelte';
	// Data
	import expensesData from './expenses';
	// variables
	let expenses = [...expensesData];
	// functions
	function removeExpense(id) {
		expenses = expenses.filter( expense => expense.id !== id ); // if the expense id matches the id it will be filtered out
	}
	// context
	setContext('state', state.remove)

	// function created for the eventDispatcher
	function deleteExpense(event) {
		console.log(event);
		const { id, name } = event.detail;
		console.log('name of event ', name);
		
		removeExpense(id)
		
	}

	function clearExpenses(){
		expenses = [];
	}

</script>

<Navbar />
<main class="content">
	<!-- <ExpensesList expenses = { expenses } removeExpense = { removeExpense }/> -->
	<ExpensesList expenses = { expenses } on:delete = { deleteExpense }/>
	<button type = "button" class="btn btn-primary btn-block" on:click={clearExpenses}>Clear expenses</button>
</main>




