<script>
  import { onMount, onDestroy } from "svelte";

  // Lucide (Svelte)
  import { ChevronLeft, ChevronRight } from "@lucide/svelte";

  import campo from '../../lib/assets/icons/campo.svg';
  import bola from '../../lib/assets/icons/bola.svg';
  import chuteira from '../../lib/assets/icons/chuteira.svg';
  import amarelo from '../../lib/assets/icons/amarelo.svg';
  import vermelho from '../../lib/assets/icons/vermelho.svg';

  // Notícias
  const noticias = [
    {
      titulo:
        "Libertadores: Conmebol divulga data de sorteio da fase de grupos",
      texto:
        "A Conmebol vai sortear os grupos da Libertadores 2025 no dia 17 de março, uma segunda-feira. Botafogo, Palmeiras, Flamengo, Internacional, São Paulo e Fortaleza estão garantidos, e Corinthians e Bahia terão que passar por dois mata-matas da fase prévia na luta por um lugar entre os 32 que estarão nas chaves."
    },
    {
      titulo:
        "Dentro da proposta de cada um, Ferroviário foi melhor que o Fortaleza no jogo de ida da semifinal",
      texto:
        "Num jogo de futebol, cada time deve ser analisado não apenas pelo que fez, mas também pelo que se propôs a fazer. E esta é a visão que nos permite concluir que, no jogo de ida da semifinal do Campeonato Cearense, neste sábado (1º), o Ferroviário foi melhor que o Fortaleza, no empate em 0 a 0, no PV."
    }
  ];

  // players (mesma lista do React)
  const players = [
    {
      id: 1,
      nome: "Tinga",
      imagem:
        "https://lncimg.lance.com.br/uploads/2023/10/Tinga-LDU-Fortaleza-scaled-aspect-ratio-512-320.jpg",
      estatisticas: [9, 1065, 754, 1, 0]
    },
    {
      id: 2,
      nome: "Vinicius Júnior",
      imagem:
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTbSoR1SCaJ4zk-2YucMv5q58ug8dWHcxrn_g&s",
      estatisticas: [8, 7, 4, 2, 1]
    },
    {
      id: 3,
      nome: "Antony",
      imagem: "https://www.netflu.com.br/wp-content/uploads/2025/02/antony.jpg",
      estatisticas: [5, 2, 4, 0, 1]
    },
    {
      id: 4,
      nome: "Cauã Felipe",
      imagem: "https://www.netflu.com.br/wp-content/uploads/2025/02/antony.jpg",
      estatisticas: [0, 0, 0, 0, 0]
    }
  ];

  // estados reativos
  let noticiaAtual = 0;
  let animando = false;
  let direcao = 1; // 1 próximo, -1 anterior

  const passarNoticia = (modo) => {
    if (animando) return;
    animando = true;
    direcao = modo === "proximo" ? 1 : -1;

    // anima por 300ms (mesmo comportamento do React)
    setTimeout(() => {
      noticiaAtual =
        modo === "proximo"
          ? (noticiaAtual + 1) % noticias.length
          : (noticiaAtual - 1 + noticias.length) % noticias.length;
      animando = false;
    }, 300);
  };

  // classe dinâmica para o container da notícia (usada no markup)
  $: noticiasTransformClass = animando
    ? direcao === 1
      ? "-translate-x-full"
      : "translate-x-full"
    : "translate-x-0";

  // autoplay (20s)
  let timer;
  onMount(() => {
    timer = setInterval(() => {
      passarNoticia("proximo");
    }, 20000);
  });
  onDestroy(() => {
    clearInterval(timer);
  });
</script>

<div class="flex wrapper min-h-screen bg-transparent text-white">
  <!-- Conteúdo Principal -->
  <div class="flex-1 flex flex-col p-4 md:p-6 lg:p-8 gap-4 md:gap-6 overflow-hidden">
    <!-- Linha Superior: Tabela e Classificação -->
    <div class="flex-1 grid grid-cols-1 lg:grid-cols-[2fr_1fr] gap-4 md:gap-6 overflow-hidden">
      <!-- Seção de Melhores Atletas -->
      <div class="flex flex-col bg-gray-950/25 backdrop-blur-md rounded-3xl border-2 border-gray-400/50 p-4 md:p-6 overflow-auto">
        <h1 class="text-xl md:text-2xl font-semibold mb-4">Melhores do Mês</h1>
        <hr class="border-gray-400/50 mb-4" />

        <!-- Cabeçalho da Tabela -->
        <div class="w-full grid grid-cols-[2.5fr_repeat(5,0.7fr)] items-center px-2 py-2 text-sm md:text-base">
          <h2 class="font-bold">Melhores Atletas</h2>

          <!-- Usando lucide (soccer-pitch, soccer-ball, sneaker) -->
          <div class="flex justify-center"><img src={campo} class="w-6 h-6 md:w-8 md:h-8" /></div>
          <div class="flex justify-center"><img src={bola} class="w-6 h-6 md:w-8 md:h-8" /></div>
          <div class="flex justify-center"><img src={chuteira} class="w-6 h-6 md:w-8 md:h-8" /></div>

          <!-- cartões amarelo/vermelho: vamos desenhar pequenos quadrados coloridos -->
          <div class="flex justify-center"><div class="w-4 h-6 rounded-sm bg-yellow-400/90"></div></div>
          <div class="flex justify-center"><div class="w-4 h-6 rounded-sm bg-red-500/90"></div></div>
        </div>

        <!-- Lista de Jogadores -->
        <ul class="w-full mt-2">
          {#each players as jogador}
            <li class="grid grid-cols-[2.5fr_repeat(5,0.7fr)] items-center px-2 py-2 hover:bg-gray-800/40 rounded-lg transition-colors cursor-pointer">
              <div class="flex items-center gap-2 md:gap-4">
                <img class="w-8 h-8 md:w-12 md:h-12 rounded-full object-cover ring-1 ring-gray-200" src={jogador.imagem} alt={jogador.nome} />
                <span class="text-sm md:text-base font-medium">{jogador.nome}</span>
              </div>

              {#each jogador.estatisticas as stat, i}
                <span class="text-center text-sm md:text-base">{stat}</span>
              {/each}
            </li>
          {/each}
        </ul>
      </div>

      <!-- Seção de Classificação -->
      <div class="flex flex-col bg-gray-950/25 backdrop-blur-md rounded-3xl border-2 border-gray-400/50 p-4 md:p-6 overflow-auto">
        <h1 class="text-xl md:text-2xl font-semibold mb-4">Rachas Próximos</h1>
        <hr class="border-gray-400/50 mb-4" />
        <!-- Conteúdo da classificação (placeholder) -->
        <div class="text-gray-400">Adicionar lista de rachas aqui</div>
      </div>
    </div>

    <!-- Seção de Notícias -->
    <div class="h-20 md:h-32 lg:h-38 bg-gray-950/25 backdrop-blur-md rounded-3xl border-2 border-gray-400/50 p-4 relative">
      <div class="flex items-center h-full gap-4">
        <button on:click={() => passarNoticia("anterior")} class="shrink-0 p-2 hover:bg-gray-800/25 rounded-full transition-colors">
          <ChevronLeft class="w-6 h-6" />
        </button>

        <div class="relative flex-1 h-full overflow-hidden">
          <div class={`absolute inset-0 flex flex-col justify-center transition-transform duration-300 ease-in-out ${noticiasTransformClass}`}>
            <h3 class="text-lg md:text-xl font-bold mb-2 line-clamp-1">{noticias[noticiaAtual].titulo}</h3>
            <p class="text-sm md:text-base line-clamp-3">{noticias[noticiaAtual].texto}</p>
          </div>
        </div>

        <button on:click={() => passarNoticia("proximo")} class="shrink-0 p-2 hover:bg-gray-800/25 rounded-full transition-colors">
          <ChevronRight class="w-6 h-6" />
        </button>
      </div>

      <span class="absolute bottom-2 left-1/2 -translate-x-1/2 text-xs text-gray-300">
        {noticiaAtual + 1}/{noticias.length}
      </span>
    </div>
  </div>
</div>
