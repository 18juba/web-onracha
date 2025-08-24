<script>
  import { onMount } from "svelte";
  import {
    ChevronRight,
    ChevronLeft,
    LayoutPanelLeft,
    Search,
    Settings,
    LogOut,
    Mail,
    CalendarDays,
    User2,
    Icon
  } from "@lucide/svelte";
  import { soccerPitch } from '@lucide/lab';

  import foto_perfil from "../../assets/img/foto_perfil.webp";

  let isHovered = false;
  let isExpanded = false;
</script>

<div
  class={`fixed z-50 top-10 left-10 flex flex-col text-wrap flex-wrap gap-4 items-center backdrop-blur-sm p-4 rounded-3xl transition-all duration-300 border-2 border-gray-400/50 
    ${
      isExpanded
        ? "w-72 h-11/12 justify-items-start bg-red-800"
        : isHovered
          ? "w-24 h-96 justify-items-start bg-red-800"
          : "w-20 h-20 justify-center bg-red-800"
    }"
  `}
  aria-roledescription="Sidebar"
  on:mouseenter={() => (isHovered = true)}
  on:mouseleave={() => (isHovered = false)}
>
  {#if isHovered && !isExpanded}
    <button class="flex cursor-pointer" on:click={() => (isExpanded = true)}>
      <ChevronRight strokeWidth={4} class="text-green-400" />
      <ChevronRight strokeWidth={4} class="text-green-400" />
    </button>
  {/if}

  {#if !isExpanded}
    <div
      class={`flex items-center justify-center rounded-full bg-green-500/10
        ${isHovered ? "p-2" : "p-1"}
      `}
    >
      <img
        class="rounded-full object-cover transition-all duration-100 cursor-pointer hover:border-4 border-green-400/90"
        alt="Avatar"
        src={foto_perfil}
      />
    </div>
  {/if}

  {#if isExpanded}
    <div class="w-full flex align-center justify-center gap-3">
      <div
        class="flex w-12 h-12 items-center justify-center rounded-full bg-green-500/10"
      >
        <img
          class="h-3/4 w-3/4 rounded-full object-cover transition-all duration-100 cursor-pointer hover:border-4 border-green-400/90"
          alt="Avatar"
          src={foto_perfil}
        />
      </div>
      <h1
        class="relative flex justify-center items-center text-sm font-bold text-white text-center text-wrap"
        style="text-shadow: 0 2px 2px green"
      >
        JORGE LUCAS
      </h1>
      <button class="flex cursor-pointer" on:click={() => (isExpanded = false)}>
        <ChevronLeft strokeWidth={4} class="w-4 text-green-400" />
        <ChevronLeft strokeWidth={4} class="w-4 text-green-400" />
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
        <a
          href="/membro"
          class={`w-full gap-3 flex items-center py-2 px-3 hover:border border-green-400/90 rounded-full cursor-pointer
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <LayoutPanelLeft />
          {#if isExpanded}<p>Central</p>{/if}
        </a>

        <a
          href="/membro/rachas"
          class={`w-full gap-3 flex items-center py-2 px-3 hover:border border-green-400/90 rounded-full cursor-pointer
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <Icon iconNode={soccerPitch}/>
          {#if isExpanded}<p>Rachas</p>{/if}
        </a>

        <a
          href="/membro/calendario"
          class={`w-full gap-3 flex items-center py-2 px-3 hover:border border-green-400/90 rounded-full cursor-pointer
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <CalendarDays />
          {#if isExpanded}<p>Calendário</p>{/if}
        </a>

        <a
          href="/membro/mensagens"
          class={`relative w-full gap-3 flex items-center py-2 px-3 hover:border border-green-400/90 rounded-full cursor-pointer
            ${isExpanded ? "justify-start" : "justify-center items-center"}
          `}
        >
          <Mail />
          <span
            class="absolute -top-0 -right-0 p-1 rounded-full text-center font-bold text-white text-xs bg-red-500/70"
          >
            {#if isExpanded}5{/if}
          </span>
          {#if isExpanded}
            <p>Mensagens</p>
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
              class={`w-full gap-3 flex items-center py-2 px-3 hover:border border-green-400/90 rounded-full cursor-pointer
                ${isExpanded ? "justify-start" : "justify-center items-center"}
              `}
            >
              <Settings />
              <p>Configurações</p>
            </li>

            <li
              class={`w-full gap-3 flex items-center py-2 px-3 hover:border border-green-400/90 rounded-full cursor-pointer
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
