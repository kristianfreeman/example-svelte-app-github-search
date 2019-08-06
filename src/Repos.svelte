<script>
  export let username

  const getRepos = async username => {
    const response = await fetch(`https://api.github.com/users/${username}/repos?per_page=100`)
    return response.json()
  }
</script>

<div class="py-4">
  {#await getRepos(username)}
    <div class="p-4 my-4 bg-white rounded-lg shadow-lg">
      <p>Loading...</p>
    </div>
  {:then repos}
    {#each repos as repo}
      <div class="p-4 my-4 bg-white rounded-lg shadow-lg">
        <h1 class="text-lg font-bold">
          <a href={repo.html_url}>{repo.name}</a>
        </h1>
        {#if repo.description}
          <h2 class="pt-4">{repo.description}</h2>
        {/if}
      </div>
    {/each}
  {:catch error}
    <p style="color: red">{error.message}</p>
  {/await}
</div>
