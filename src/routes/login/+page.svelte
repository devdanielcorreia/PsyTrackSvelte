<script lang="ts">
  import { signIn } from '$lib/auth';

  let email = '';
  let password = '';
  let message = '';

  const handleLogin = async () => {
    message = 'Entrando...';
    try {
      await signIn(email, password);
      message = 'Login realizado com sucesso!';
    } catch (err: any) {
      message = 'Erro: ' + err.message;
    }
  };
</script>

<section class="flex items-center justify-center min-h-screen bg-gray-50">
  <div class="card w-full max-w-sm space-y-6">
    <h1 class="text-center text-2xl font-bold text-gray-800">Login PsyTrackSvelte</h1>

    <form on:submit|preventDefault={handleLogin} class="space-y-4">
      <div>
        <label class="block text-sm font-medium text-gray-700">Email</label>
        <input
          type="email"
          bind:value={email}
          placeholder="seu@email.com"
          class="input-base"
        />
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700">Senha</label>
        <input
          type="password"
          bind:value={password}
          placeholder="********"
          class="input-base"
        />
      </div>

      <button type="submit" class="btn-primary w-full">
        Entrar
      </button>
    </form>

    <p class="text-center text-sm text-gray-600">{message}</p>
  </div>
</section>
