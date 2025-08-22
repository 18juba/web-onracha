<script>
  // Dados mockados organizados por meses
  const mockJogos = [
    {
      status: "agendado",
      data: { mes: 3, dia: 5 },
      time1: {
        logo: "https://upload.wikimedia.org/wikipedia/pt/thumb/4/41/Logotipo_do_SBT.svg/800px-Logotipo_do_SBT.svg.png",
        placar: null,
      },
      time2: {
        logo: "https://logodetimes.com/times/fortaleza/logo-fortaleza-256.png",
        placar: null,
      },
      horario: "9:30",
    },
    {
      status: "finalizado",
      data: { mes: 1, dia: 15 },
      time1: {
        logo: "https://logodetimes.com/times/avai/logo-avai-256.png",
        placar: 1,
      },
      time2: {
        logo: "https://logodetimes.com/times/fortaleza/logo-fortaleza-256.png",
        placar: 2,
      },
      horario: "16:00",
    },
    {
      status: "finalizado",
      data: { mes: 2, dia: 10 },
      time1: {
        logo: "https://logodetimes.com/times/fortaleza/logo-fortaleza-256.png",
        placar: 2,
      },
      time2: {
        logo: "https://logodetimes.com/times/gremio/logo-gremio-256.png",
        placar: 1,
      },
      horario: "19:00",
    },
    {
      status: "finalizado",
      data: { mes: 1, dia: 3 },
      time1: {
        logo: "https://logodetimes.com/times/fortaleza/logo-fortaleza-256.png",
        placar: 2,
      },
      time2: {
        logo: "https://logodetimes.com/times/red-bull-bragantino/logo-red-bull-bragantino-256.png",
        placar: 1,
      },
      horario: "20:00",
    },
    {
      status: "agendado",
      data: { mes: 3, dia: 15 },
      time1: {
        logo: "https://logodetimes.com/times/red-bull-bragantino/logo-red-bull-bragantino-256.png",
        placar: null,
      },
      time2: {
        logo: "https://logodetimes.com/times/fortaleza/logo-fortaleza-256.png",
        placar: null,
      },
      horario: "9:30",
    },
  ];

  // Configuração dos meses
  const mesesConfig = [
    { nome: "Janeiro", numero: 1, dias: 31 },
    { nome: "Fevereiro", numero: 2, dias: 28 },
    { nome: "Março", numero: 3, dias: 31 },
    { nome: "Abril", numero: 4, dias: 30 },
    { nome: "Maio", numero: 5, dias: 31 },
    { nome: "Junho", numero: 6, dias: 30 },
    { nome: "Julho", numero: 7, dias: 31 },
    { nome: "Agosto", numero: 8, dias: 31 },
    { nome: "Setembro", numero: 9, dias: 30 },
    { nome: "Outubro", numero: 10, dias: 31 },
    { nome: "Novembro", numero: 11, dias: 30 },
    { nome: "Dezembro", numero: 12, dias: 31 },
  ];

  // Estado → mês atual
  let mesSelecionado = new Date().getMonth() + 1;

  // Dia atual
  const hoje = new Date();
  const diaAtual = hoje.getDate();
  const mesAtualSistema = hoje.getMonth() + 1;

  // Reativos
  $: jogosDoMes = mockJogos.filter((jogo) => jogo.data.mes === mesSelecionado);
  $: mesAtual = mesesConfig.find((mes) => mes.numero === mesSelecionado);
</script>

<div class="flex wrapper min-h-screen bg-transparent text-white">
  <!-- Conteúdo Principal -->
  <div class="flex-1 flex flex-col p-4 md:p-6 lg:p-8 gap-4 overflow-auto">
    <!-- Cabeçalho -->
    <div class="flex flex-col md:flex-row justify-between items-center gap-4">
      <h1 class="text-2xl md:text-3xl font-bold">{mesAtual.nome}</h1>
      <select
        class="bg-gray-800 rounded-lg px-4 py-2 text-sm md:text-base"
        bind:value={mesSelecionado}
      >
        {#each mesesConfig as mes}
          <option value={mes.numero}>{mes.nome}</option>
        {/each}
      </select>
    </div>

    <hr class="my-4 border-gray-400/50" />

    <!-- Grid de Dias -->
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-7 gap-4">
      {#each Array.from({ length: mesAtual.dias }, (_, i) => i + 1) as dia}
        {@const jogo = jogosDoMes.find((j) => j.data.dia === dia)}
        {@const ehDiaAtual = dia === diaAtual && mesSelecionado === mesAtualSistema}

        <div
          class={`flex flex-col justify-between p-4 h-40 rounded-3xl border-2 cursor-pointer overflow-hidden transition-all duration-300
            ${ehDiaAtual ? "inset-shadow-sm inset-shadow-blue-700 border-blue-600 bg-blue-400/10" : ""}
            ${
              !ehDiaAtual && jogo
                ? jogo.status === "agendado"
                  ? "border-green-400/90 hover:border-green-400 hover:bg-green-400/10"
                  : "border-gray-200/80"
                : "border-gray-400/50"
            }`}
        >
          <h1
            class={`font-bold ${jogo ? "text-lg md:text-xl" : "text-xl"} ${
              ehDiaAtual ? "text-blue-400" : ""
            }`}
          >
            {dia}
          </h1>

          <div class="flex-1 flex flex-col justify-center items-center">
            {#if jogo}
              <div class="flex flex-col items-center justify-center">
                <div class="flex gap-5 justify-center items-center p-1">
                  {#if jogo.status === "agendado"}
                    <img
                      class="w-10 h-10 md:w-12 md:h-12 object-cover"
                      src={jogo.time1.logo}
                      alt="Time 1"
                    />
                    <h1 class="text-xl md:text-2xl font-bold text-center">X</h1>
                    <img
                      class="w-10 h-10 md:w-12 md:h-12 object-cover"
                      src={jogo.time2.logo}
                      alt="Time 2"
                    />
                  {:else}
                    <div class="flex gap-2 justify-center items-center">
                      <div class="flex justify-center items-center">
                        <img
                          class="w-10 h-10 md:w-12 md:h-12 object-cover"
                          src={jogo.time1.logo}
                          alt="Time 1"
                        />
                        <h1 class="text-sm md:text-base font-bold">
                          {jogo.time1.placar}
                        </h1>
                      </div>
                      <h1 class="text-sm md:text-base font-bold text-center">X</h1>
                      <div class="flex items-center">
                        <h1 class="text-sm md:text-base font-bold">
                          {jogo.time2.placar}
                        </h1>
                        <img
                          class="w-10 h-10 md:w-12 md:h-12 object-cover"
                          src={jogo.time2.logo}
                          alt="Time 2"
                        />
                      </div>
                    </div>
                  {/if}
                </div>
                <h1 class="text-center text-lg md:text-xl font-bold">
                  {jogo.horario}
                </h1>
              </div>
            {/if}
          </div>
        </div>
      {/each}
    </div>
  </div>
</div>
