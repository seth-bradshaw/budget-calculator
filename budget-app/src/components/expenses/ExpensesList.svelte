<script>
  import { fly } from "svelte/transition";
  import { flip } from "svelte/animate";
  import Title from "./Title.svelte";
  import Expense from "./Expense.svelte";

  export let expenses = [];
</script>

<main>
  <section>
    <Title title="expenses list" />
    <ul>
      {#each expenses as expense, index (expense.id)}
        <div
          in:fly={{ x: 200, delay: (index + 1) * 400 }}
          out:fly={{ x: -200 }}
          animate:flip
        >
          <Expense {expense} on:remove />
        </div>
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
