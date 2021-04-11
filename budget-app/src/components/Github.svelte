<script>
  import { onMount } from "svelte";

  let users = [];
  let isLoading = true;

  onMount(async () => {
    let userData = await fetch("http://api.github.com/users");
    let githubUsers = await userData.json();
    users = githubUsers;
    isLoading = false;
  });
</script>

<main>
  {#if isLoading}
    <h2>Loading...</h2>
  {:else}
    <section>
      {#each users as user}
        <article class="user">
          <img src={user.avatar_url} alt={user.login} />
          <div class="user-info">
            <h3>User: {user.login}</h3>
            <a href={user.html_url} class="btn-primary" target="_blank"
              >github url</a
            >
          </div>
        </article>
      {/each}
    </section>
  {/if}
</main>

<style>
  h2 {
    text-align: center;
  }
</style>
