<script lang="ts">
  import '../styles/globals.css'
  import { supabase } from '$lib/supabaseClient'
  import { signOut } from '$lib/auth'
  import { onMount } from 'svelte'

  let session = null

  onMount(async () => {
    const { data } = await supabase.auth.getSession()
    session = data.session
  })

  supabase.auth.onAuthStateChange((_, _session) => {
    session = _session
  })

  const handleLogout = async () => {
    await signOut()
    session = null
  }
</script>

<main class="min-h-screen bg-gray-50 text-gray-900 font-sans flex flex-col">
  <nav class="flex justify-between items-center px-6 py-3 shadow-sm bg-white border-b border-gray-200">
    <h1 class="text-lg font-semibold text-gray-700">PsyTrackSvelte</h1>
    {#if session}
      <div class="flex items-center space-x-4">
        <p class="text-sm text-gray-600">{session.user.email}</p>
        <button
          on:click={handleLogout}
          class="text-sm text-blue-600 hover:underline"
        >
          Sair
        </button>
      </div>
    {/if}
  </nav>

  <section class="flex-1">
    <slot />
  </section>
</main>


