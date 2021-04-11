<script>
  import Github from "./components/Github.svelte";
  import GithubAwait from "./components/GithubAwait.svelte";
  import NavBar from "./components/navigation/Navbar.svelte";
  import Title from "./components/expenses/Title.svelte";
  import Modal from "./components/modals/Modal.svelte";
  import Totals from "./components/expenses/Totals.svelte";
  import ExpenseForm from "./components/expenses/ExpenseForm.svelte";
  import ExpensesList from "./components/expenses/ExpensesList.svelte";
  import { setContext, onMount, afterUpdate } from "svelte";

  let expenses = [];
  let setName = "";
  let setAmount = null;
  let setId = null;

  let isFormOpen = false;

  $: isEditing = setId;
  $: total = expenses.reduce((acc, cur) => {
    return (acc += cur.amount);
  }, 0);

  // const removeExpense = (id) => {
  //   expenses = expenses.filter((expense) => expense.id !== id);
  // };

  const removeExpense = (event) => {
    expenses = expenses.filter((expense) => expense.id !== event.detail);
  };

  const clearExpenses = () => {
    expenses = [];
  };

  const addExpense = ({ name, amount }) => {
    let expense = { id: Math.random() * Date.now(), name, amount };
    expenses = [expense, ...expenses];
  };

  const setModifiedExpense = (id) => {
    let expense = expenses.find((item) => item.id === id);

    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    console.log(expense, { setId, setName, setAmount });
  };

  const editExpense = ({ name, amount }) => {
    expenses = expenses.map((item) => {
      if (item.id === setId) {
        return { ...item, name, amount };
      } else {
        return item;
      }
    });
    setId = null;
    setAmount = null;
    setName = "";
  };

  const showForm = () => {
    isFormOpen = true;
  };

  const closeForm = () => {
    isFormOpen = false;
    setId = null;
    setAmount = null;
    setName = "";
  };

  setContext("delete", removeExpense);
  setContext("modify", setModifiedExpense);

  const setLocalStorage = () => {
    localStorage.setItem("expenses", JSON.stringify(expenses));
  };

  onMount(() => {
    expenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];
  });

  afterUpdate(() => {
    setLocalStorage();
  });
</script>

<NavBar {showForm} />
<main class="content">
  <!-- <Github /> -->
  <GithubAwait />
  <!-- {#if isFormOpen || isEditing}
    <Modal>
      <ExpenseForm
        {addExpense}
        name={setName}
        amount={setAmount}
        {isEditing}
        {editExpense}
        {closeForm}
      />
    </Modal>
  {/if}
  <Totals title="total expenses" {total} />
  <ExpensesList {expenses} on:remove={removeExpense} />
  <button
    type="button"
    class="btn btn-primary btn-block"
    on:click={clearExpenses}>clear expenses</button
  > -->
</main>

<style>
</style>
