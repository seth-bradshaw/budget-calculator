<script>
  import NavBar from "./components/navigation/Navbar.svelte";
  import Title from "./components/expenses/Title.svelte";
  import sampleExpenses from "./seedData.js";
  import ExpensesList from "./components/expenses/ExpensesList.svelte";
  import { setContext } from "svelte";

  let fruits = ["apple", "orange", "lemon"];
  let expenses = [...sampleExpenses];

  const removeExpense = (id) => {
    expenses = expenses.filter((expense) => expense.id !== id);
  };

  const removeExpense2 = (event) => {
    expenses = expenses.filter((expense) => expense.id !== event.detail);
  };

  setContext("delete", removeExpense);
</script>

<main>
  <NavBar />
  <ExpensesList {expenses} on:remove={removeExpense2} />
</main>

<style>
</style>
