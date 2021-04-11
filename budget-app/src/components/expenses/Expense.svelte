<script>
  import { getContext, createEventDispatcher } from "svelte";
  import { blur, slide, scale, fade, fly } from "svelte/transition";
  export let expense = {};

  let displayAmount = false;

  const toggleDetails = () => (displayAmount = !displayAmount);

  const removeExpense = getContext("delete");
  const editExpense = getContext("modify");
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
        <h4 transition:slide>
          amount : ${expense.amount}
        </h4>
      {/if}
    </div>
    <div class="expense-buttons">
      <button class="expense-bttn edit-btn"
        ><i
          class="fas fa-pen"
          on:click={() => editExpense(expense.id)}
        /></button
      >
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
