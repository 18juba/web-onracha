<script>
  import { Eye, EyeOff } from "@lucide/svelte";
  import { goto } from "$app/navigation";
  import logo from '../../lib/assets/img/on_racha_logo.png';

  let showPassword = false;
  let email = "";
  let password = "";
  let remember = false;

  function login() {
    console.log({ email, password, remember });
    // Aqui você pode chamar sua API de login
    goto("/");
  }
</script>

<div
  class="min-h-screen bg-gradient-to-br from-slate-900 via-emerald-900 to-slate-900 flex items-center justify-center p-4"
>
  <div class="w-full max-w-md relative z-1">
    <div
      class="absolute inset-0 bg-gradient-to-r from-cyan-400/20 to-emerald-400/20 rounded-full blur-3xl -z-1"
    ></div>
    <img alt="Logo" src={logo} class="w-60 mb-8 mx-auto"/>
    <div
      class="bg-slate-800/50 border border-emerald-500/30 backdrop-blur-sm rounded-lg shadow-lg"
    >
      <div class="text-center p-6">
        <h2 class="text-2xl font-bold text-white">Bem-vindo de volta</h2>
        <p class="text-gray-300">Entre na sua conta para continuar</p>
      </div>

      <div class="p-6 space-y-6">
        <!-- Email -->
        <div class="space-y-2">
          <label for="email" class="text-white">Email</label>
          <input
            id="email"
            type="email"
            bind:value={email}
            placeholder="seu@email.com"
            class="w-full bg-slate-700/50 border border-emerald-500/30 text-white rounded px-3 py-2 placeholder:text-gray-400 focus:border-cyan-400"
          />
        </div>

        <!-- Senha -->
        <div class="space-y-2">
          <label for="password" class="text-white">Senha</label>
          <div class="relative">
            <input
              id="password"
              type={showPassword ? "text" : "password"}
              bind:value={password}
              placeholder="Sua senha"
              class="w-full bg-slate-700/50 border border-emerald-500/30 text-white rounded px-3 py-2 pr-10 placeholder:text-gray-400 focus:border-cyan-400"
            />
            <button
              type="button"
              on:click={() => (showPassword = !showPassword)}
              class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-cyan-400"
            >
              {#if showPassword}
                <EyeOff class="h-4 w-4" />
              {:else}
                <Eye class="h-4 w-4" />
              {/if}
            </button>
          </div>
        </div>

        <!-- Lembrar e Esqueceu a senha -->
        <div class="flex items-center justify-between">
          <div class="flex items-center space-x-2">
            <input
              id="remember"
              type="checkbox"
              bind:checked={remember}
              class="rounded border-emerald-500/30 bg-slate-700/50 text-cyan-500 focus:ring-cyan-400"
            />
            <label for="remember" class="text-sm text-gray-300"
              >Lembrar de mim</label
            >
          </div>
          <a
            href="/recuperar_senha"
            class="text-sm text-cyan-400 hover:text-cyan-300 transition-colors"
          >
            Esqueceu a senha?
          </a>
        </div>

        <!-- Botão entrar -->
        <button
          on:click={login}
          class="w-full bg-cyan-500 hover:bg-cyan-600 text-white rounded px-4 py-2 font-medium cursor-pointer"
        >
          Entrar
        </button>

        <!-- Link cadastro -->
        <div class="text-center">
          <p class="text-gray-300">
            Não tem uma conta?
            <a
              href="/cadastro"
              class="text-cyan-400 hover:text-cyan-300 transition-colors font-medium"
            >
              Cadastre-se
            </a>
          </p>
        </div>
      </div>
    </div>

    <div class="text-center mt-6">
      <a
        href="/"
        class="text-gray-400 hover:text-cyan-400 transition-colors text-sm"
      >
        ← Voltar para o início
      </a>
    </div>
  </div>
</div>
