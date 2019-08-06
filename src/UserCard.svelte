<script>
  export let username
  const getUser = async username => {
    const response = await fetch(`https://api.github.com/users/${username}`)
    return response.json()
  }
</script>

<div class="p-4 bg-white rounded-lg flex shadow-lg">
  {#await getUser(username)}
    <div>Loading...</div>
  {:then user}
    <div>
      <img alt={user.login} src={user.avatar_url} style="max-width: 150px" />
    </div>
    <div class="px-6">
      <h1 class="text-2xl font-bold">
        <a href={user.html_url}>{user.name}</a>
      </h1>
      <h2 class="text-gray-700 text-lg pb-4">@{user.login}</h2>
      {#if user.bio}
        <p class="text-sm">{user.bio}</p>
      {/if}
    </div>
  {/await}
</div>
