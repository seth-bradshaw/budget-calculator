<script>
  import { getContext, createEventDispatcher } from "svelte";
  export let expense = {};

  let displayAmount = false;

  const toggleDetails = () => (displayAmount = !displayAmount);

  const removeExpense = getContext("delete");
  const dispatch = createEventDispatcher();
</script>

<main>
  <article class="single-expense">
    <div class="expense-info">
      <h2>
        {expense.name}
        <button class="amount-btn" on:click={toggleDetails}
          ><i class="fas fa-caret-down" /></button
        >
      </h2>
      {#if displayAmount}
        <h4>amount : ${expense.amount}</h4>
      {/if}
    </div>
    <div class="expense-buttons">
      <button class="expense-bttn edit-btn"><i class="fas fa-pen" /></button>
      <!-- <button
        class="expense-bttn delete-btn"
        on:click={() => removeExpense(expense.id)}
        ><i class="fas fa-trash" /></button
      > -->
      <button
        class="expense-bttn delete-btn"
        on:click={() => dispatch("remove", expense.id)}
        ><i class="fas fa-trash" /></button
      >
    </div>
  </article>
</main>
