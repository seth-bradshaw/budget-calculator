<script>
  import Title from "./Title.svelte";
  import Expense from "./Expense.svelte";

  export let expenses = [];
</script>

<main>
  <section>
    <Title title="expenses list" />
    <ul>
      {#each expenses as expense}
        <Expense {expense} on:remove />
      {:else}
        <h2>no expenses are on the list</h2>
      {/each}
    </ul>
  </section>
</main>

<style>
  h2 {
    text-transform: capitalize;
  }
</style>
