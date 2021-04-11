<script>
  import Title from "./Title.svelte";
  export let addExpense;
  export let name = "";
  export let amount = null;
  export let isEditing;
  export let editExpense;
  export let closeForm;

  const handleSubmit = () => {
    if (!isEditing) {
      addExpense({ name, amount });
    } else {
      editExpense({ name, amount });
    }
    name = "";
    amount = null;
    closeForm();
  };

  $: isEmpty = !name || !amount;
</script>

<section class="form">
  <Title title="add expense" />
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">please fill out all form fields</p>
    {/if}
    <button
      type="submit"
      class="btn btn-block"
      class:disabled={isEmpty}
      disabled={isEmpty}>{isEditing ? "edit" : "add"} expense</button
    >
    <button class="close-btn" type="button">
      <i class="fas fa-times" on:click={closeForm}> close</i></button
    >
  </form>
</section>
