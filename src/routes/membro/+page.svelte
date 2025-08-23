<script>
  import { onMount, onDestroy } from "svelte";

  // Lucide (Svelte)
  import {
    ChevronLeft,
    ChevronRight,
    ChevronDown,
    Star,
    Icon,
    MapPin,
    Calendar,
    Clock,
    MoreHorizontal,
    Users
  } from "@lucide/svelte";
  import { soccerPitch } from "@lucide/lab";

  import campo from "../../lib/assets/icons/campo.svg";
  import bola from "../../lib/assets/icons/bola.svg";
  import chuteira from "../../lib/assets/icons/chuteira.svg";
  import amarelo from "../../lib/assets/icons/amarelo.svg";
  import vermelho from "../../lib/assets/icons/vermelho.svg";

  // Notícias
  const noticias = [
    {
      titulo:
        "Libertadores: Conmebol divulga data de sorteio da fase de grupos",
      texto:
        "A Conmebol vai sortear os grupos da Libertadores 2025 no dia 17 de março, uma segunda-feira. Botafogo, Palmeiras, Flamengo, Internacional, São Paulo e Fortaleza estão garantidos, e Corinthians e Bahia terão que passar por dois mata-matas da fase prévia na luta por um lugar entre os 32 que estarão nas chaves.",
    },
    {
      titulo:
        "Dentro da proposta de cada um, Ferroviário foi melhor que o Fortaleza no jogo de ida da semifinal",
      texto:
        "Num jogo de futebol, cada time deve ser analisado não apenas pelo que fez, mas também pelo que se propôs a fazer. E esta é a visão que nos permite concluir que, no jogo de ida da semifinal do Campeonato Cearense, neste sábado (1º), o Ferroviário foi melhor que o Fortaleza, no empate em 0 a 0, no PV.",
    },
  ];

  const arenas = [
    {
      id: 1,
      nome: "Arena Goleada",
      imagem:
        "https://www.baratocoletivo.com.br/static/team/2016/1010/14761334341290.jpg",
      estatisticas: [9.8, 1065, 432],
    },
    {
      id: 2,
      nome: "Villa's Society",
      imagem:
        "https://www.futebol7brasil.com.br/images/noticias/1148/579a9b74b412fba1fe6ede690185a56b.jpg",
      estatisticas: [8.9, 1299, 389],
    },
    {
      id: 3,
      nome: "Se7e",
      imagem:
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTZjb_qy2PT7n2lt-4Gk215Xx-Z0pFF-UBNOw&s",
      estatisticas: [9, 789, 295],
    },
    {
      id: 4,
      nome: "Estádio Presidente Vargas",
      imagem:
        "https://www.fortaleza.ce.gov.br/images/images1/00008M/BeiraMar/21%2005%202022%20PV%20(25).JPG",
      estatisticas: [10, 5, 41],
    },
  ];

  const nearbyArenas = [
    {
      id: 1,
      name: "Arena V3",
      location: "Rodolfo Teófilo",
      nextGame: "Hoje, 19:00",
      status: "Disponível",
      players: "9/15",
      price: "R$ 15",
    },
    {
      id: 2,
      name: "Estádio Presidente Vargas",
      location: "Benfica",
      nextGame: "Amanhã, 18:30",
      status: "Lotando",
      players: "38/40",
      price: "R$ 899",
    },
    {
      id: 3,
      name: "Se7e",
      location: "Bairro de Fátima",
      nextGame: "29/08/2025 20:30",
      status: "Disponível",
      players: "10/16",
      price: "R$ 18",
    },
    {
      id: 4,
      name: "Arena Fontenele",
      location: "Jardim América",
      nextGame: "30/08/2025 20:30",
      status: "Lotado",
      players: "14/14",
      price: "R$ 15",
    },
  ];

  let openMenu = null;

  function toggleMenu(id) {
    openMenu = openMenu === id ? null : id;
  }

  let noticiaAtual = 0;
  let animando = false;
  let direcao = 1;

  const passarNoticia = (modo) => {
    if (animando) return;
    animando = true;
    direcao = modo === "proximo" ? 1 : -1;

    setTimeout(() => {
      noticiaAtual =
        modo === "proximo"
          ? (noticiaAtual + 1) % noticias.length
          : (noticiaAtual - 1 + noticias.length) % noticias.length;
      animando = false;
    }, 300);
  };

  $: noticiasTransformClass = animando
    ? direcao === 1
      ? "-translate-x-full"
      : "translate-x-full"
    : "translate-x-0";

  let timer;
  onMount(() => {
    timer = setInterval(() => {
      passarNoticia("proximo");
    }, 10000);
  });
  onDestroy(() => {
    clearInterval(timer);
  });
</script>

<div class="flex wrapper min-h-screen bg-transparent text-white">
  <div
    class="flex-1 flex flex-col gap-4 md:gap-6 overflow-hidden"
  >
    <div
      class="flex-1 grid grid-cols-1 lg:grid-cols-[2fr_1fr] gap-4 md:gap-6 overflow-hidden"
    >
      <div
        class="flex flex-col bg-gray-950/25 backdrop-blur-md rounded-3xl border-2 border-gray-400/50 p-4 md:p-6 overflow-auto"
      >
        <h1 class="text-xl md:text-2xl font-semibold mb-4">Melhores de 2025</h1>
        <hr class="border-gray-400/50 mb-4" />

        <div
          class="w-full grid grid-cols-[2.5fr_repeat(3,0.7fr)] items-center px-2 py-2 text-sm md:text-base"
        >
          <h2 class="font-bold flex gap-2">
            Top Arenas <ChevronDown class="cursor-pointer" />
          </h2>
          <div class="flex flex-col justify-center items-center">
            <Star class="w-6 h-6 md:w-8 md:h-8" />
            <p class="text-xs">Nota</p>
          </div>
          <div class="flex flex-col justify-center items-center">
            <Icon class="w-6 h-6 md:w-8 md:h-8" iconNode={soccerPitch} />
            <p class="text-xs">Jogos</p>
          </div>
          <div class="flex flex-col justify-center items-center">
            <img src={chuteira} class="w-6 h-6 md:w-8 md:h-8" />
            <p class="text-xs">Participantes</p>
          </div>
        </div>

        <!-- Lista de arenas -->
        <ul class="w-full mt-2">
          {#each arenas as arena}
            <li
              class="grid grid-cols-[2.5fr_repeat(3,0.7fr)] items-center px-2 py-2 hover:bg-gray-800/40 rounded-lg transition-colors cursor-pointer"
            >
              <div class="flex items-center gap-2 md:gap-4">
                <img
                  class="w-8 h-8 md:w-12 md:h-12 rounded-full object-cover ring-1 ring-gray-200"
                  src={arena.imagem}
                  alt={arena.nome}
                />
                <span class="text-sm md:text-base font-medium"
                  >{arena.nome}</span
                >
              </div>

              {#each arena.estatisticas as stat, i}
                <span class="text-center text-sm md:text-base">{stat}</span>
              {/each}
            </li>
          {/each}
        </ul>
      </div>

      <!-- Seção de Classificação -->
      <div
        class="bg-gray-950/25 border-2 border-gray-400/50 backdrop-blur-sm rounded-3xl p-2"
      >
        <div class="p-4 border-b border-emerald-800/50">
          <h2 class="text-white text-xl font-semibold">Rachas Próximos</h2>
          <p class="text-emerald-300 text-sm">
            Arenas próximas disponíveis para jogar
          </p>
        </div>
        <div class="p-4 overflow-x-auto">
          <table class="w-full text-sm">
            <thead>
              <tr
                class="border-b border-emerald-800/50 text-emerald-300 text-left"
              >
                <th class="py-2">
                  <div class="flex items-center gap-2">
                    <MapPin class="h-4 w-4" /> Arena
                  </div>
                </th>
                <th class="py-2">
                  <div class="flex items-center gap-2">
                    <Clock class="h-4 w-4" /> Próximo Jogo
                  </div>
                </th>
                <th class="py-2">Status</th>
                <th class="py-2 text-right">Ações</th>
              </tr>
            </thead>
            <tbody>
              {#each nearbyArenas as arena}
                <tr
                  class="border-b border-emerald-800/30 hover:bg-emerald-900/20"
                >
                  <td class="py-3">
                    <div class="space-y-1">
                      <div class="text-white font-medium">{arena.name}</div>
                      <div
                        class="text-emerald-300 text-sm flex items-center gap-1"
                      >
                        <MapPin class="h-3 w-3" />
                        {arena.location}
                      </div>
                      <div class="text-emerald-400 text-xs">{arena.price}</div>
                    </div>
                  </td>
                  <td class="py-3">
                    <div class="space-y-1">
                      <div class="text-white text-sm flex items-center gap-1">
                        <Calendar class="h-3 w-3" />
                        {arena.nextGame}
                      </div>
                      <div
                        class="text-emerald-300 text-xs flex items-center gap-1"
                      >
                        <Users class="h-3 w-3" />
                        {arena.players} jogadores
                      </div>
                    </div>
                  </td>
                  <td class="py-3">
                    <span
                      class="px-2 py-1 text-xs font-semibold rounded-full
                      {arena.status === 'Disponível'
                        ? 'bg-emerald-600 text-white'
                        : arena.status === 'Lotando'
                          ? 'bg-yellow-600 text-white'
                          : 'bg-red-600 text-white'}"
                    >
                      {arena.status}
                    </span>
                  </td>
                  <td class="py-3 text-right relative">
                    <button
                      class="h-8 w-8 flex items-center justify-center rounded-full text-emerald-300 hover:bg-emerald-900/30 hover:text-white"
                      on:click={() => toggleMenu(arena.id)}
                    >
                      <MoreHorizontal class="h-4 w-4" />
                    </button>

                    {#if openMenu === arena.id}
                      <div
                        class="fixed z-50 right-0 mt-2 w-40 bg-emerald-950 border border-emerald-800 rounded-lg shadow-lg"
                      >
                        <button
                          class="w-full text-left px-4 py-2 text-emerald-100 hover:bg-emerald-900"
                          >Ver Detalhes</button
                        >
                        <button
                          class="w-full text-left px-4 py-2 text-emerald-100 hover:bg-emerald-900"
                          >Jogar</button
                        >
                        <button
                          class="w-full text-left px-4 py-2 text-emerald-100 hover:bg-emerald-900"
                          >Compartilhar</button
                        >
                      </div>
                    {/if}
                  </td>
                </tr>
              {/each}
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- Seção de Notícias -->
    <div
      class="h-20 md:h-32 lg:h-38 bg-gray-950/25 backdrop-blur-md rounded-3xl border-2 border-gray-400/50 p-4 relative"
    >
      <div class="flex items-center h-full gap-4">
        <button
          on:click={() => passarNoticia("anterior")}
          class="shrink-0 p-2 hover:bg-gray-800/25 rounded-full transition-colors"
        >
          <ChevronLeft class="w-6 h-6" />
        </button>

        <div class="relative flex-1 h-full overflow-hidden">
          <div
            class={`absolute inset-0 flex flex-col justify-center transition-transform duration-300 ease-in-out ${noticiasTransformClass}`}
          >
            <h3 class="text-lg md:text-xl font-bold mb-2 line-clamp-1">
              {noticias[noticiaAtual].titulo}
            </h3>
            <p class="text-sm md:text-base line-clamp-3">
              {noticias[noticiaAtual].texto}
            </p>
          </div>
        </div>

        <button
          on:click={() => passarNoticia("proximo")}
          class="shrink-0 p-2 hover:bg-gray-800/25 rounded-full transition-colors"
        >
          <ChevronRight class="w-6 h-6" />
        </button>
      </div>

      <span
        class="absolute bottom-2 left-1/2 -translate-x-1/2 text-xs text-gray-300"
      >
        {noticiaAtual + 1}/{noticias.length}
      </span>
    </div>
  </div>
</div>
