<script lang="ts">
  import {currentUser, pb} from './pocketbase'

  let username: string
  let password: string

  async function login() {
    const user = await pb.collection('users').authWithPassword(username, password)
    console.log(user)
  }

  async function signUp() {
    try {
      const data = {
        username,
        password,
        passwordConfirm: password,
        name: 'hi dad!'
      }
      const createdUser = await pb.collection('users').create(data)
      await login()
    } catch (err) {
      console.log(err)
    }
  }

  function signOut() {
    pb.authStore.clear()
  }
</script>

{#if $currentUser}
  <p>
    Signed in as {$currentUser.username}
    <button on:click={signOut}>Sign Out</button>
  </p>
{:else}
  <form on:submit|preventDefault>
    <input 
      type="text"
      placeholder="Username"
      bind:value={username}
    >

    <input
      placeholder="Password"
      type="password"
      bind:value={password}
    >
    <button on:click={signUp}>Sign Up</button>
    <button on:click={login}>Login</button>
  </form>
{/if}
