<script>
	import { setContext } from 'svelte';
	const state = {
		name: 'simple name',
		remove: removeExpense 
	}
	// Components
	import Navbar from './Navbar.svelte';
	import ExpensesList from './ExpensesList.svelte';
	import Totals from './Totals.svelte';
	import ExpenseForm from './ExpenseForm.svelte';
	// Data
	import expensesData from './expenses';
	// variables
	let expenses = [...expensesData];
	// set Editing Variables
	let setName='';
	let setAmount=null;
	let setId=null;
	// toggle form variables
	let isFormOpen = false;
	// reactives (variables/computed properties)
	$: total = expenses.reduce((acc,cur)=> acc+=cur.amount, 0);
	$: isEditing = setId?true:false; 
	// functions
	function showForm(){
		isFormOpen = true;
	}

	function hideForm(){
		isFormOpen = false;
		setId=null;
		setName='';
		setAmount=null;
	}

	function removeExpense(id) {
		expenses = expenses.filter( expense => expense.id !== id ); // if the expense id matches the id it will be filtered out
	}

	function clearExpenses(){
		expenses = [];
	}

	function addExpense({name, amount}) {
		console.log(name, amount);
		let expense = {
			id: Math.random*Date.now(),
			name,
			amount
		}
		expenses = [expense, ...expenses];
	}

	function setModifiedExpense(id) {
		let expense = expenses.find(item => item.id === id);
		// console.log(expense);
		setId = expense.id;
		setName = expense.name;
		setAmount = expense.amount;
		// console.log({setId, setName, setAmount});
		showForm();
	}

	// function created for the eventDispatcher
	function deleteExpense(event) {
		console.log(event);
		const { id, name } = event.detail;
		console.log('name of event ', name);
		removeExpense(id)
	}

	function editExpense({name, amount}){
		// console.log(name, amount);
		expenses = expenses.map( item => {
			// does my item.id match the setId
			return item.id === setId ? {...item, name, amount} : item
			// return item.id === setId ? {...item, name:name, amount:amount} : {...item}
		});
		setId = null;
		setAmount: null;
		setName: '';
	}
	// context
	setContext('state', state.remove)
	setContext('modify', setModifiedExpense)

</script>

<Navbar { showForm }/>
<main class="content">
	{#if isFormOpen}
		<ExpenseForm 
			addExpense={addExpense} 
			name={setName} 
			amount={setAmount} 
			isEditing={isEditing}
			editExpense={editExpense}
			hideForm = {hideForm}
		/>
	{/if}
	<Totals title="total expenses" total={total}/>
	<!-- <ExpensesList expenses = { expenses } removeExpense = { removeExpense }/> -->
	<ExpensesList expenses = { expenses } on:delete = { deleteExpense }/>
	<button type = "button" class="btn btn-primary btn-block" on:click={clearExpenses}>Clear expenses</button>
</main>




