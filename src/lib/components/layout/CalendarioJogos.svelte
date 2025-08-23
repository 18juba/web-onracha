<script>
  const gamesData = [
    {
      date: 5,
      games: [
        {
          id: 1,
          arena: "Arena Goleada",
          time: "9:30",
          arenaImage:
            "https://www.baratocoletivo.com.br/static/team/2016/1010/14761334341290.jpg",
          location: "Vila Madalena",
        },
      ],
    },
    {
      date: 15,
      games: [
        {
          id: 2,
          arena: "Villa's Society",
          time: "19:40",
          arenaImage:
            "https://www.futebol7brasil.com.br/images/noticias/1148/579a9b74b412fba1fe6ede690185a56b.jpg",
          location: "Barroso",
        },
      ],
    },
    {
      date: 22,
      games: [
        {
          id: 3,
          arena: "Se7e Sports",
          time: "18:40",
          arenaImage:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTZjb_qy2PT7n2lt-4Gk215Xx-Z0pFF-UBNOw&s",
          location: "Bairro de Fátima",
        },
        {
          id: 4,
          arena: "No Alvo",
          time: "22:00",
          arenaImage:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRzSSlvh2EhxazDn8F74UcP0QGHHqvkeeKJuw&s",
          location: "José Walter",
        },
      ],
    },
    {
      date: 28,
      games: [
        {
          id: 5,
          arena: "Estádio Presidente Vargas",
          time: "20:30",
          arenaImage:
            "https://www.fortaleza.ce.gov.br/images/images1/00008M/BeiraMar/21%2005%202022%20PV%20(25).JPG",
          location: "Benfica",
        },
      ],
    },
  ];

  const months = [
    "Janeiro",
    "Fevereiro",
    "Março",
    "Abril",
    "Maio",
    "Junho",
    "Julho",
    "Agosto",
    "Setembro",
    "Outubro",
    "Novembro",
    "Dezembro",
  ];

  let currentDate = new Date();
  let selectedMonth = currentDate.getMonth();
  const selectedYear = currentDate.getFullYear();
  let selectedDayGames = [];
  let isModalOpen = false;

  let monthDropdownOpen = false;

  const getGamesForDay = (day) =>
    (gamesData.find((g) => g.date === day) || {}).games ?? [];

  function getDaysInMonth(month, year) {
    const lastDay = new Date(year, month + 1, 0);
    const daysInMonth = lastDay.getDate();
    return Array.from({ length: daysInMonth }, (_, i) => i + 1);
  }

  function handleCardClick(day, games) {
    // só abre modal quando há múltiplos jogos (como no original)
    if (games.length > 1) {
      selectedDayGames = games;
      isModalOpen = true;
    }
  }

  $: days = getDaysInMonth(selectedMonth, selectedYear);
  $: today = currentDate.getDate();
  $: currentMonth = currentDate.getMonth();

  function onWindowClick() {
    monthDropdownOpen = false;
  }

  function onKeydown(e) {
    if (e.key === "Escape") {
      isModalOpen = false;
    }
  }
</script>

<svelte:window on:click={onWindowClick} on:keydown={onKeydown} />

<!-- container -->
<div class="px-6">
  <!-- Header: título + dropdown -->
  <div class="flex items-center justify-between mb-6">
    <h1 class="text-white text-3xl font-bold">{months[selectedMonth]}</h1>

    <!-- Dropdown custom -->
    <div class="relative">
      <button
        class="text-white hover:bg-emerald-800/50 flex items-center gap-2 px-3 py-1 rounded"
        on:click|stopPropagation={() =>
          (monthDropdownOpen = !monthDropdownOpen)}
        aria-haspopup="true"
        aria-expanded={monthDropdownOpen}
      >
        <span>{months[selectedMonth]}</span>
        <!-- ChevronDown SVG -->
        <svg
          class="h-4 w-4"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
        >
          <path
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 9l6 6 6-6"
          />
        </svg>
      </button>

      {#if monthDropdownOpen}
        <div
          class="absolute right-0 mt-2 w-56 bg-emerald-950 border border-emerald-800 rounded shadow-lg z-50"
          on:click|stopPropagation
        >
          {#each months as month, index}
            <div
              class="px-4 py-2 cursor-pointer text-emerald-100 hover:bg-emerald-900 hover:text-white"
              on:click={() => {
                selectedMonth = index;
                monthDropdownOpen = false;
              }}
            >
              {month}
            </div>
          {/each}
        </div>
      {/if}
    </div>
  </div>

  <hr class="my-8 border-gray-400/50" />

  <!-- Grid de dias -->
  <div class="grid grid-cols-7 gap-4">
    {#each days as day}
      {@const games = getGamesForDay(day)}
      {@const hasGames = games.length > 0}
      {@const hasMultipleGames = games.length > 1}
      {@const isToday = day === today && selectedMonth === currentMonth}

      <div
        class={`bg-emerald-950/10 border-2 backdrop-blur-sm h-36 p-3 relative overflow-hidden transition-all duration-200 rounded-2xl
            ${isToday ? "border-cyan-400" : "border-gray-400/50"}
            ${hasGames ? "border-emerald-600" : ""}
            ${hasMultipleGames ? "border-yellow-500 border-2 cursor-pointer hover:bg-emerald-900/30" : ""}`}
        on:click={() => handleCardClick(day, games)}
      >
        <div class="h-full flex flex-col">
          <div class="text-white font-semibold text-lg">{day}</div>

          {#if hasGames}
            <div class="flex-1 flex flex-col justify-center items-center">
              {#each games.slice(0, 1) as game}
                <div class="flex flex-col items-center text-center space-y-2">
                  <div class="flex items-center gap-2">
                    <img
                      src={game.arenaImage ?? "/placeholder.svg"}
                      alt={game.arena}
                      class="w-6 h-6 rounded-full object-cover"
                    />
                    <span class="text-white font-medium text-sm truncate"
                      >{game.arena}</span
                    >
                  </div>

                  <div class="flex items-center gap-1 text-emerald-300">
                    <!-- MapPin icon -->
                    <svg
                      class="w-3 h-3"
                      viewBox="0 0 24 24"
                      fill="none"
                      stroke="currentColor"
                    >
                      <path
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M21 10c0 6-9 12-9 12S3 16 3 10a9 9 0 1118 0z"
                      />
                      <circle
                        cx="12"
                        cy="10"
                        r="3"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                      />
                    </svg>
                    <span class="text-xs">{game.location}</span>
                  </div>

                  <div class="flex items-center gap-1 text-emerald-300">
                    <!-- Clock icon -->
                    <svg
                      class="w-3 h-3"
                      viewBox="0 0 24 24"
                      fill="none"
                      stroke="currentColor"
                    >
                      <circle
                        cx="12"
                        cy="12"
                        r="10"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                      />
                      <path
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M12 6v6l4 2"
                      />
                    </svg>
                    <span class="text-sm font-medium">{game.time}</span>
                  </div>
                </div>
              {/each}

              {#if hasMultipleGames}
                <div
                  class="absolute top-2 right-2 bg-yellow-500 text-black text-xs px-2 py-1 rounded-full font-bold"
                >
                  +{games.length - 1}
                </div>
              {/if}
            </div>
          {/if}
        </div>
      </div>
    {/each}
  </div>

  {#if isModalOpen}
    <div
      class="fixed inset-0 z-50 flex items-center justify-center"
      role="dialog"
      aria-modal="true"
    >
      <div
        class="absolute inset-0 bg-black/60"
        on:click={() => (isModalOpen = false)}
      ></div>

      <div class="relative max-w-md w-full mx-4">
        <div
          class="bg-emerald-950 border border-emerald-800 text-white rounded-lg overflow-hidden"
        >
          <div class="p-4 border-b border-emerald-800">
            <h2 class="text-emerald-300 text-lg font-semibold">Jogos do Dia</h2>
          </div>

          <div class="p-4 space-y-4">
            {#each selectedDayGames as game}
              <div
                class="bg-emerald-900/50 rounded-lg p-4 border border-emerald-800"
              >
                <div class="flex items-center gap-3 mb-3">
                  <img
                    src={game.arenaImage ?? "/placeholder.svg"}
                    alt={game.arena}
                    class="w-8 h-8 rounded-full object-cover"
                  />
                  <div>
                    <h3 class="text-white font-semibold">{game.arena}</h3>
                    <div
                      class="flex items-center gap-1 text-emerald-300 text-sm"
                    >
                      <!-- MapPin small -->
                      <svg
                        class="w-3 h-3"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                      >
                        <path
                          stroke-width="2"
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          d="M21 10c0 6-9 12-9 12S3 16 3 10a9 9 0 1118 0z"
                        />
                        <circle
                          cx="12"
                          cy="10"
                          r="3"
                          stroke-width="2"
                          stroke-linecap="round"
                          stroke-linejoin="round"
                        />
                      </svg>
                      <span>{game.location}</span>
                    </div>
                  </div>
                </div>

                <div class="flex items-center gap-1 text-emerald-300">
                  <!-- Clock -->
                  <svg
                    class="w-4 h-4"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                  >
                    <circle
                      cx="12"
                      cy="12"
                      r="10"
                      stroke-width="2"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    />
                    <path
                      stroke-width="2"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M12 6v6l4 2"
                    />
                  </svg>
                  <span class="font-medium">{game.time}</span>
                </div>
              </div>
            {/each}
          </div>

          <div class="p-3 border-t border-emerald-800 flex justify-end gap-2">
            <button
              class="px-3 py-1 rounded bg-emerald-800 hover:bg-emerald-700 text-white"
              on:click={() => (isModalOpen = false)}
            >
              Fechar
            </button>
          </div>
        </div>
      </div>
    </div>
  {/if}

  <!-- Legenda -->
  <div class="mt-6 flex items-center justify-center gap-6 text-sm">
    <div class="flex items-center gap-2">
      <div
        class="w-4 h-4 bg-emerald-950/50 border border-emerald-400 rounded"
      ></div>
      <span class="text-emerald-300">Dia atual</span>
    </div>
    <div class="flex items-center gap-2">
      <div
        class="w-4 h-4 bg-emerald-950/50 border border-emerald-600 rounded"
      ></div>
      <span class="text-emerald-300">Com jogos agendados</span>
    </div>
    <div class="flex items-center gap-2">
      <div
        class="w-4 h-4 bg-emerald-950/50 border-2 border-yellow-500 rounded"
      ></div>
      <span class="text-emerald-300">Múltiplos jogos (clique para ver)</span>
    </div>
  </div>
</div>
