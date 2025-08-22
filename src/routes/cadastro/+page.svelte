<script lang="ts">
  import { Crown, Eye, EyeOff, User, Building } from "@lucide/svelte";
  import { goto } from "$app/navigation";

  let showPassword = false;
  let showConfirmPassword = false;
  let userType = "";
  let firstName = "";
  let lastName = "";
  let email = "";
  let phone = "";
  let password = "";
  let confirmPassword = "";
  let terms = false;

  function criarConta() {
    if (!terms) {
      alert("Você precisa aceitar os termos para continuar.");
      return;
    }
    console.log({
      userType,
      firstName,
      lastName,
      email,
      phone,
      password,
      confirmPassword,
    });
    // Aqui você pode chamar sua API
    goto("/login");
  }
</script>

<div
  class="min-h-screen bg-gradient-to-br from-slate-900 via-emerald-900 to-slate-900 flex items-center justify-center p-4"
>
  <div class="w-full max-w-md">
    <!-- Logo -->
    <div class="flex items-center justify-center gap-2 mb-8">
      <Crown class="h-8 w-8 text-cyan-400" />
      <span class="text-2xl font-bold text-white">ArenaBook</span>
    </div>

    <div
      class="bg-slate-800/50 border border-emerald-500/30 backdrop-blur-sm rounded-lg shadow-lg"
    >
      <div class="text-center p-6">
        <h2 class="text-2xl font-bold text-white">Criar conta</h2>
        <p class="text-gray-300">Junte-se à nossa comunidade esportiva</p>
      </div>

      <div class="p-6 space-y-6">
        <!-- Tipo de usuário -->
        <div class="space-y-2">
          <label for="userType" class="text-white">Tipo de usuário</label>
          <select
            bind:value={userType}
            id="userType"
            class="w-full bg-slate-700/50 border border-emerald-500/30 text-white rounded px-3 py-2 focus:border-cyan-400"
          >
            <option value="" disabled>Selecione o tipo de usuário</option>
            <option value="jogador">Jogador</option>
            <option value="proprietario">Proprietário</option>
          </select>
        </div>

        <!-- Nome / Sobrenome -->
        <div class="grid grid-cols-2 gap-4">
          <div class="space-y-2">
            <label for="firstName" class="text-white">Nome</label>
            <input
              id="firstName"
              bind:value={firstName}
              placeholder="Seu nome"
              class="w-full bg-slate-700/50 border border-emerald-500/30 text-white rounded px-3 py-2 placeholder:text-gray-400 focus:border-cyan-400"
            />
          </div>
          <div class="space-y-2">
            <label for="lastName" class="text-white">Sobrenome</label>
            <input
              id="lastName"
              bind:value={lastName}
              placeholder="Seu sobrenome"
              class="w-full bg-slate-700/50 border border-emerald-500/30 text-white rounded px-3 py-2 placeholder:text-gray-400 focus:border-cyan-400"
            />
          </div>
        </div>

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

        <!-- Telefone -->
        <div class="space-y-2">
          <label for="phone" class="text-white">Telefone</label>
          <input
            id="phone"
            type="tel"
            bind:value={phone}
            placeholder="(11) 99999-9999"
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
              placeholder="Crie uma senha forte"
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

        <!-- Confirmar senha -->
        <div class="space-y-2">
          <label for="confirmPassword" class="text-white">Confirmar senha</label
          >
          <div class="relative">
            <input
              id="confirmPassword"
              type={showConfirmPassword ? "text" : "password"}
              bind:value={confirmPassword}
              placeholder="Confirme sua senha"
              class="w-full bg-slate-700/50 border border-emerald-500/30 text-white rounded px-3 py-2 pr-10 placeholder:text-gray-400 focus:border-cyan-400"
            />
            <button
              type="button"
              on:click={() => (showConfirmPassword = !showConfirmPassword)}
              class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-cyan-400"
            >
              {#if showConfirmPassword}
                <EyeOff class="h-4 w-4" />
              {:else}
                <Eye class="h-4 w-4" />
              {/if}
            </button>
          </div>
        </div>

        <!-- Termos -->
        <div class="flex items-center space-x-2">
          <input
            id="terms"
            type="checkbox"
            bind:checked={terms}
            class="rounded border-emerald-500/30 bg-slate-700/50 text-cyan-500 focus:ring-cyan-400"
          />
          <label for="terms" class="text-sm text-gray-300">
            Aceito os <a
              href="/termos"
              class="text-cyan-400 hover:text-cyan-300">termos de uso</a
            >
            e
            <a href="/privacidade" class="text-cyan-400 hover:text-cyan-300">
              política de privacidade</a
            >
          </label>
        </div>

        <!-- Botão criar conta -->
        <button
          on:click={criarConta}
          class="w-full bg-cyan-500 hover:bg-cyan-600 text-white rounded px-4 py-2 font-medium"
        >
          Criar conta
        </button>

        <!-- Link login -->
        <div class="text-center">
          <p class="text-gray-300">
            Já tem uma conta?
            <a
              href="/login"
              class="text-cyan-400 hover:text-cyan-300 transition-colors font-medium"
              >Faça login</a
            >
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
