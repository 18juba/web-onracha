<script>
  import { onMount } from "svelte";

  import { EllipsisVertical, CheckCircle } from "@lucide/svelte";

  // Mock de dados
  const Dados = [
    {
      id: 1,
      userId: 1,
      titulo: "Jogo de Hoje",
      texto: "Hoje tem jogo se prepare",
      data: "2025/03/06 00:00:00",
      lida: false,
    },
    {
      id: 2,
      userId: 1,
      titulo: "Inscrição",
      texto: "Você foi inscrito no SBT Futebol Clube",
      data: "2025/03/08",
      lida: false,
    },
    {
      id: 3,
      userId: 1,
      titulo: "Jogo de Hoje",
      texto: "Hoje tem jogo se prepare",
      data: "2025/03/17 00:00:00",
      lida: false,
    },
  ];

  // Estado
  let notificacoes = [...Dados];
  let currentPage = 1;
  const itemsPerPage = 5;
  let showMenuId = null;
  let deletingIds = [];

  // Marcar todas como lidas
  function marcarTodasComoLidas() {
    notificacoes = notificacoes.map((n) => ({ ...n, lida: true }));
  }

  // Fechar menu ao clicar fora
  onMount(() => {
    const handleClickOutside = (e) => {
      if (!e.target.closest(".menu-container")) {
        showMenuId = null;
      }
    };
    document.addEventListener("click", handleClickOutside);
    return () => document.removeEventListener("click", handleClickOutside);
  });

  // Paginação
  $: indexOfLastItem = currentPage * itemsPerPage;
  $: indexOfFirstItem = indexOfLastItem - itemsPerPage;
  $: currentItems = notificacoes.slice(indexOfFirstItem, indexOfLastItem);

  function paginate(pageNumber) {
    currentPage = pageNumber;
  }

  // Alternar lida
  function toggleLida(id) {
    notificacoes = notificacoes.map((n) =>
      n.id === id ? { ...n, lida: !n.lida } : n
    );
  }

  // Excluir notificação
  function deleteNotificacao(id) {
    deletingIds = [...deletingIds, id];
    setTimeout(() => {
      notificacoes = notificacoes.filter((n) => n.id !== id);
      deletingIds = deletingIds.filter((d) => d !== id);
    }, 300);
  }
</script>

<div class="flex wrapper min-h-screen bg-transparent text-white">
  <div
    class="flex-1 flex flex-col gap-4 overflow-auto"
  >
    <!-- Cabeçalho -->
    <div class="flex flex-col md:flex-row justify-between items-center gap-4">
      <h1 class="text-2xl md:text-3xl font-bold flex items-center gap-2">
        Mensagens
      </h1>

      <button
        on:click={marcarTodasComoLidas}
        class="flex items-center gap-2 bg-gray-800 hover:bg-gray-700 rounded-lg px-4 py-2 transition-colors duration-200 cursor-pointer"
      >
        <CheckCircle class="w-5 h-5 text-green-400" />
        <span class="hidden md:block">Marcar todas como lidas</span>
      </button>
    </div>

    <hr class="my-4 border-gray-400/50" />

    <!-- Lista de notificações -->
    <div class="grid grid-cols-1 gap-4">
      {#if currentItems.length === 0}
        <div class="text-center py-12 text-gray-400">
          Nenhuma notificação encontrada
        </div>
      {:else}
        {#each currentItems as notificacao}
          <div
            class={`flex flex-col p-4 rounded-3xl border-2 transition-all duration-300 relative
              ${!notificacao.lida ? "border-blue-400/80 bg-blue-400/10" : "border-gray-600/50 bg-gray-800/30"}
              ${deletingIds.includes(notificacao.id) ? "animate-fade-out" : "animate-fade-in"}
              ${showMenuId === notificacao.id ? "z-30" : "z-0"}`}
          >
            <div class="flex justify-between items-start">
              <div class="flex items-center gap-2">
                {#if !notificacao.lida}
                  <div
                    class="w-2 h-2 bg-blue-400 rounded-full animate-pulse"
                  ></div>
                {/if}

                <h2 class="text-lg md:text-xl font-bold">
                  {notificacao.titulo}
                </h2>
              </div>

              <div class="flex items-center gap-3">
                <span class="text-sm text-gray-400">
                  {new Date(notificacao.data).toLocaleDateString("pt-BR", {
                    day: "2-digit",
                    month: "long",
                    year: "numeric",
                  })}
                </span>

                <div class="relative menu-container">
                  <EllipsisVertical
                    class="w-5 h-5 text-gray-500 hover:text-gray-300 transition-colors cursor-pointer relative z-10"
                    on:click={(e) => {
                      e.stopPropagation();
                      showMenuId =
                        notificacao.id === showMenuId ? null : notificacao.id;
                    }}
                  />

                  {#if showMenuId === notificacao.id}
                    <div
                      class="absolute right-0 top-6 bg-gray-800 rounded-lg p-2 shadow-lg z-40"
                    >
                      <button
                        class="block w-full text-left px-4 py-2 hover:bg-gray-700 rounded-lg cursor-pointer"
                        on:click={(e) => {
                          e.stopPropagation();
                          deleteNotificacao(notificacao.id);
                          showMenuId = null;
                        }}
                      >
                        Excluir
                      </button>
                      <button
                        class="block w-full text-left px-4 py-2 hover:bg-gray-700 rounded-lg cursor-pointer"
                        on:click={(e) => {
                          e.stopPropagation();
                          toggleLida(notificacao.id);
                          showMenuId = null;
                        }}
                      >
                        {notificacao.lida
                          ? "Marcar como não lida"
                          : "Marcar como lida"}
                      </button>
                    </div>
                  {/if}
                </div>
              </div>
            </div>

            <p class="text-gray-300 text-sm md:text-base mt-2">
              {notificacao.texto}
            </p>
          </div>
        {/each}
      {/if}
    </div>

    <!-- Paginação -->
    {#if notificacoes.length > itemsPerPage}
      <div class="flex justify-center gap-2 mt-6">
        <button
          class={`px-4 py-2 rounded-lg ${
            currentPage === 1
              ? "bg-gray-800 cursor-not-allowed"
              : "bg-gray-800 hover:bg-gray-700"
          }`}
          on:click={() => paginate(currentPage - 1)}
          disabled={currentPage === 1}
        >
          Anterior
        </button>
        <button
          class={`px-4 py-2 rounded-lg ${
            indexOfLastItem >= notificacoes.length
              ? "bg-gray-800 cursor-not-allowed"
              : "bg-gray-800 hover:bg-gray-700"
          }`}
          on:click={() => paginate(currentPage + 1)}
          disabled={indexOfLastItem >= notificacoes.length}
        >
          Próximo
        </button>
      </div>
    {/if}
  </div>
</div>
