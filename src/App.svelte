<script>
  import UserCard from './UserCard.svelte'
  import Repos from './Repos.svelte'

  let username = 'signalnerve'
  const changeUsername = evt => (username = evt.target.value)
</script>

<div class="flex flex-col items-center mx-auto" style="width: 500px; max-width: 500px">
  <input
    class="p-4 mb-8 rounded-lg"
    value={username}
    on:change={changeUsername}
    placeholder="Search a GitHub username" />

  {#if username}
    <div>
      <UserCard {username} />
      <Repos {username} />
    </div>
  {/if}
</div>
