<script>
  import { user } from './sessionStore'
  import { supabase } from './supabaseClient'
  import Auth from './Auth.svelte'
  import Profile from './Profile.svelte'

  user.set(supabase.auth.user())

  supabase.auth.onAuthStateChange((_, session) => {
    user.set(session.user)
  })

  $: console.log($user)
</script>

<main>
  <div>
    {#if $user}
      <Profile />
    {:else}
      <Auth />
    {/if}
  </div>
</main>

<style>
  main {
    max-width: 601px;
    margin: 2rem auto;
  }
  div {
    padding: 50px 0 100px 0;
  }
  @media screen and (max-width: 600px) {
    main {
      max-width: 80%;
    }
  }
</style>
