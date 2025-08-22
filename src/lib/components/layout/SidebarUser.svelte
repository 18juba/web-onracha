<script>
  import { onMount } from "svelte";
  import {
    ChevronRight,
    ChevronLeft,
    Home,
    Search,
    Settings,
    LogOut,
    Bell,
    Calendar,
    User2,
  } from "@lucide/svelte";

  let isHovered = false;
  let isExpanded = false;
</script>

<div
  class={`font1 fixed z-50 top-10 left-10 flex backdrop-blur-sm flex-col items-center text-wrap flex-wrap gap-4 px-4 rounded-3xl transition-all duration-300 border-2 border-gray-400/50 
    ${
      isExpanded
        ? "w-72 h-11/12 py-4 justify-items-start bg-black/15"
        : isHovered
          ? "w-24 h-96 py-4 justify-items-start bg-green-800/25"
          : "w-20 h-20 justify-center bg-gray-800/15"
    }
  `}
  on:mouseenter={() => (isHovered = true)}
  on:mouseleave={() => (isHovered = false)}
>
  {#if isHovered && !isExpanded}
    <button class="flex cursor-pointer" on:click={() => (isExpanded = true)}>
      <ChevronRight class="text-green-400" />
      <ChevronRight class="text-green-400" />
    </button>
  {/if}

  {#if !isExpanded}
    <div
      class={`flex items-center justify-center rounded-full bg-green-500/10
        ${isExpanded ? "h-20 w-20" : isHovered ? "h-16 w-16" : "h-12 w-12"}
      `}
    >
      <div
        class="h-3/4 w-3/4 rounded-full object-cover transition-all duration-100 cursor-pointer hover:border-4 border-green-400/90"
        alt="Avatar"
      >
        <User2 />
      </div>
    </div>
  {/if}

  {#if isExpanded}
    <div class="w-full flex align-center justify-center gap-3">
      <div
        class="flex w-12 h-12 items-center justify-center rounded-full bg-green-500/10"
      >
        <div
          class="h-3/4 w-3/4 rounded-full object-cover transition-all duration-100 cursor-pointer hover:border-4 border-green-400/90"
          alt="Avatar"
        >
          <User2 />
        </div>
      </div>
      <h1
        class="relative flex justify-center items-center text-sm font-bold text-white text-center text-wrap"
        style="text-shadow: 0 2px 2px green"
      >
        Cristiano Ronaldo
      </h1>
      <button class="flex cursor-pointer" on:click={() => (isExpanded = false)}>
        <ChevronLeft class="w-4 text-green-400" />
        <ChevronLeft class="w-4 text-green-400" />
      </button>
    </div>
  {/if}

  {#if isExpanded || isHovered}
    <div class="flex flex-col gap-3 w-full justify-center items-center">
      <hr class="w-full h-0.5 bg-slate-400/90" />
      <ul
        class={`w-full text-green-400/95 font-bold text-left flex flex-col gap-3 ${
          isExpanded
            ? "justify-start items-start"
            : "justify-center items-center"
        }`}
      >
        <li
          class={`w-full h-10 gap-3 flex justify-center items-center p-4 bg-gray-500/20 hover:border-2 border-green-400/90 rounded-full cursor-text
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <Search />
          {#if isExpanded}<p>Pesquisa</p>{/if}
        </li>

        <a
          href="/"
          class={`w-full h-10 gap-3 flex items-center p-4 hover:border border-green-400/90 rounded-full cursor-pointer
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <Home />
          {#if isExpanded}<p>Central</p>{/if}
        </a>

        <a
          href="/calendario"
          class={`w-full h-10 gap-3 flex items-center p-4 hover:border border-green-400/90 rounded-full cursor-pointer
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <Calendar />
          {#if isExpanded}<p>Jogos</p>{/if}
        </a>

        <a
          href="/notificacoes"
          class={`w-full h-10 gap-3 flex items-center p-4 hover:border border-green-400/90 rounded-full cursor-pointer
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <Bell />
          {#if isExpanded}
            <p class="flex justify-between items-center">
              Notificações
              <span
                class="w-6 h-5 ml-14 flex justify-center items-center py-2 font-bold text-white text-xs bg-red-500/70 rounded-lg"
              >
                5
              </span>
            </p>
          {/if}
        </a>
      </ul>

      {#if isExpanded}
        <div class="w-full flex flex-col gap-3 mt-1">
          <hr class="w-full h-0.5 bg-slate-400/90" />
          <ul
            class="w-full text-green-400/95 font-bold text-left flex flex-col gap-3"
          >
            <li
              class={`w-full h-10 gap-3 flex items-center p-4 hover:border border-green-400/90 rounded-full cursor-pointer
                ${isExpanded ? "justify-start" : "justify-center items-center"}
              `}
            >
              <Settings />
              <p>Configurações</p>
            </li>

            <li
              class={`w-full h-10 gap-3 flex items-center p-4 hover:border border-green-400/90 rounded-full cursor-pointer
                ${isExpanded ? "justify-start" : "justify-center items-center"}
              `}
            >
              <LogOut />
              <p>Sair</p>
            </li>
          </ul>
        </div>
      {/if}
    </div>
  {/if}

  {#if isExpanded}
    <div class="text-white">Abrido</div>
  {/if}
</div>
