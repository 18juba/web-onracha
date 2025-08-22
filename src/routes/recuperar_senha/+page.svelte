<script lang="ts">
  import { Crown, Mail, ArrowLeft } from "@lucide/svelte";

  let email = "";
  let emailSent = false;

  function enviarEmail() {
    if (!email) {
      alert("Digite seu email.");
      return;
    }
    // Simular envio de email
    emailSent = true;
  }

  function reenviarEmail() {
    emailSent = false;
    email = "";
  }
</script>

<div class="min-h-screen bg-gradient-to-br from-slate-900 via-emerald-900 to-slate-900 flex items-center justify-center p-4">
  <div class="w-full max-w-md">
    <!-- Logo -->
    <div class="flex items-center justify-center gap-2 mb-8">
      <Crown class="h-8 w-8 text-cyan-400" />
      <span class="text-2xl font-bold text-white">ArenaBook</span>
    </div>

    <div class="bg-slate-800/50 border border-emerald-500/30 backdrop-blur-sm rounded-lg shadow-lg">
      <div class="text-center p-6">
        <h2 class="text-2xl font-bold text-white">
          {#if emailSent}
            Email enviado!
          {:else}
            Recuperar senha
          {/if}
        </h2>
        <p class="text-gray-300">
          {#if emailSent}
            Verifique sua caixa de entrada para redefinir sua senha
          {:else}
            Digite seu email para receber as instruções de recuperação
          {/if}
        </p>
      </div>

      <div class="p-6 space-y-6">
        {#if !emailSent}
          <!-- Formulário de envio -->
          <div class="space-y-2">
            <label for="email" class="text-white">Email</label>
            <input
              id="email"
              type="email"
              bind:value={email}
              placeholder="seu@email.com"
              required
              class="w-full bg-slate-700/50 border border-emerald-500/30 text-white rounded px-3 py-2 placeholder:text-gray-400 focus:border-cyan-400"
            />
          </div>

          <button
            on:click={enviarEmail}
            class="w-full bg-cyan-500 hover:bg-cyan-600 text-white rounded px-4 py-2 flex items-center justify-center gap-2 font-medium"
          >
            <Mail class="h-4 w-4" />
            Enviar instruções
          </button>

          <div class="text-center">
            <p class="text-gray-300">
              Lembrou da senha?
              <a href="/login" class="text-cyan-400 hover:text-cyan-300 transition-colors font-medium">
                Fazer login
              </a>
            </p>
          </div>
        {:else}
          <!-- Mensagem de email enviado -->
          <div class="text-center space-y-6">
            <div class="bg-emerald-500/20 border border-emerald-500/30 rounded-lg p-4">
              <Mail class="h-12 w-12 text-emerald-400 mx-auto mb-3" />
              <p class="text-emerald-100 text-sm">
                Enviamos um link de recuperação para seu email. Verifique também a pasta de spam.
              </p>
            </div>

            <div class="space-y-3">
              <button
                on:click={reenviarEmail}
                class="w-full border border-cyan-400 text-cyan-400 hover:bg-cyan-400 hover:text-white rounded px-4 py-2 font-medium bg-transparent"
              >
                Enviar novamente
              </button>

              <a href="/login" class="w-full block">
                <button class="w-full bg-cyan-500 hover:bg-cyan-600 text-white rounded px-4 py-2 flex items-center justify-center gap-2 font-medium">
                  <ArrowLeft class="h-4 w-4" />
                  Voltar ao login
                </button>
              </a>
            </div>
          </div>
        {/if}
      </div>
    </div>

    <div class="text-center mt-6">
      <a href="/" class="text-gray-400 hover:text-cyan-400 transition-colors text-sm">
        ← Voltar para o início
      </a>
    </div>
  </div>
</div>
