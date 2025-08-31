<script>
  import logo from "../lib/assets/img/on_racha_logo.png";
  import {
    CalendarDays,
    MapPin,
    Users,
    Crown,
    Play,
    Trophy,
    Check,
  } from "@lucide/svelte";
  import premiere_gif from "../lib/assets/img/artilheiro.gif";
  import premiere_gif2 from "../lib/assets/img/premiere2.gif";
  import premiere_gif3 from "../lib/assets/img/premiere3.gif";
  import cta_img from "../lib/assets/img/lucero.png";
</script>

<div
  class="min-h-screen bg-gradient-to-br from-slate-900 via-emerald-900 to-slate-900 pt-28"
>
  <!-- Header -->
  <header
    class="absolute top-0 w-full z-50 px-8 py-4 bg-gradient-to-br from-emerald-700/25 to-emerald-800/25 rounded-b-3xl"
  >
    <div
      class="absolute inset-0 bg-gradient-to-r from-cyan-400/5 to-emerald-400/5 rounded-full blur-3xl"
    ></div>

    <nav class="flex items-center justify-between">
      <img alt="Logo" src={logo} class="w-60 cursor-pointer" />
      <div class="hidden md:flex items-center gap-6">
        <a
          href="#features"
          class="text-gray-300 hover:text-cyan-400 transition-colors"
          >Recursos</a
        >
        <a
          href="#about"
          class="text-gray-300 hover:text-cyan-400 transition-colors">Sobre</a
        >
        <a
          href="#contact"
          class="text-gray-300 hover:text-cyan-400 transition-colors">Contato</a
        >
      </div>
      <a href="/membro" data-sveltekit-preload-data>
        <button
          class="bg-cyan-500 hover:bg-cyan-600 text-white px-4 py-2 rounded-md cursor-pointer"
          >Entrar</button
        >
      </a>
    </nav>
  </header>

  <!-- Hero Section -->
  <section class="container mx-auto px-4 py-20">
    <div class="grid lg:grid-cols-2 gap-12 items-center">
      <div>
        <h1 class="text-2xl lg:text-4xl font-bold text-white mb-6">
          <span class="text-cyan-400">Modernizando o Esporte</span>
        </h1>
        <p class="text-xl text-gray-300 mb-8 leading-relaxed">
          Plataforma completa para proprietários de quadras registrarem suas
          arenas e usuários agendarem jogos. Conecte jogadores, organize
          partidas e gerencie sua arena com facilidade.
        </p>
        <div class="flex flex-col sm:flex-row gap-4">
          <a href="/membro" data-sveltekit-preload-data>
            <button
              class="flex items-center justify-center gap-2 bg-cyan-500 hover:bg-cyan-600 text-white px-8 py-3 rounded-lg cursor-pointer"
            >
              <Play class="h-5 w-5" />
              Começar Agora
            </button>
          </a>
          <button
            class="px-8 py-3 rounded-lg border border-cyan-400 text-cyan-400 hover:bg-cyan-400 hover:text-white bg-transparent cursor-pointer"
          >
            Saiba Mais
          </button>
        </div>
      </div>

      <div class="relative">
        <div
          class="absolute inset-0 bg-gradient-to-r from-cyan-400/20 to-emerald-400/20 rounded-full blur-3xl"
        ></div>
        <div
          class="relative bg-gradient-to-br from-cyan-600 to-cyan-800 rounded-2xl p-8 border border-emerald-500/30"
        >
          <div class="flex items-center justify-center mb-6">
            <div class="bg-cyan-500 rounded-full p-4">
              <Trophy class="h-12 w-12 text-white" />
            </div>
          </div>
          <h3 class="text-2xl font-bold text-white text-center mb-4">
            Sua Arena, Seus Jogos
          </h3>
          <p class="text-emerald-100 text-center">
            Gerencie reservas, organize torneios e conecte a comunidade
            esportiva local
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Features Section -->
  <section id="features" class="container mx-auto px-4 py-20">
    <div class="text-center mb-16">
      <h2 class="text-4xl font-bold text-white mb-4">
        <span class="text-cyan-400">RECURSOS</span> PRINCIPAIS
      </h2>
      <p class="text-xl text-gray-300 max-w-2xl mx-auto">
        Tudo que você precisa para gerenciar sua arena e organizar jogos
        inesquecíveis
      </p>
    </div>

    <div class="flex flex-col gap-12">
      <!-- Card 1 (imagem esquerda / texto direita) -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-stretch">
        <!-- imagem -->
        <div class="relative rounded-md border-2 border-emerald-500/40">
          <img
            src={premiere_gif}
            alt="Comunidade ativa"
            class="object-cover w-full h-full rounded-md"
          />
        </div>
        <!-- texto -->
        <div
          class="bg-gradient-to-t from-cyan-500/20 to-slate-900 border border-emerald-500/40 rounded-md p-6 flex flex-col justify-between"
        >
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-3xl font-bold text-white">Comunidade Ativa</h3>
            <div class="bg-cyan-500 rounded-full p-2">
              <Users class="h-5 w-5 text-white" />
            </div>
          </div>
          <p class="text-gray-100 leading-relaxed mb-4">
            Participe de uma comunidade que respira esporte. Encontre novos
            parceiros de jogo, entre em partidas abertas e crie sua própria
            equipe sem complicação.
          </p>
          <ul class="mt-auto text-gray-200 space-y-2">
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-cyan-400" strokeWidth={3} /> Jogos abertos
              sempre disponíveis
            </li>
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-emerald-400" strokeWidth={3} /> Chat entre
              jogadores
            </li>
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-cyan-400" strokeWidth={3} /> Criação de
              grupos
            </li>
          </ul>
        </div>
      </div>

      <!-- Card 2 (texto esquerda / imagem direita) -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-stretch">
        <!-- texto -->
        <div
          class="order-2 md:order-1 bg-gradient-to-t from-cyan-500/20 to-slate-900 border border-emerald-500/40 rounded-md p-6 flex flex-col justify-between"
        >
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-3xl font-bold text-white">Registro de Arenas</h3>
            <div class="bg-cyan-500 rounded-full p-2">
              <MapPin class="h-5 w-5 text-white" />
            </div>
          </div>
          <p class="text-gray-300 leading-relaxed mb-4">
            Dê visibilidade à sua arena! Proprietários podem cadastrar quadras
            com fotos, preços e horários em tempo real, atraindo mais jogadores
            para o seu espaço.
          </p>
          <ul class="mt-auto text-gray-100 text-lg space-y-2">
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-emerald-400" strokeWidth={3} /> Cadastro
              rápido e simples
            </li>
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-cyan-400" strokeWidth={3} /> Agenda atualizada
              automaticamente
            </li>
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-emerald-400" strokeWidth={3} /> Maior alcance
              na comunidade
            </li>
          </ul>
        </div>
        <!-- imagem -->
        <div
          class="order-1 md:order-2 relative rounded-md border-2 border-emerald-500/40"
        >
          <img
            src={premiere_gif2}
            alt="Registro de arenas"
            class="object-cover w-full h-full rounded-md"
          />
        </div>
      </div>

      <!-- Card 3 (imagem esquerda / texto direita) -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-stretch">
        <!-- imagem -->
        <div class="relative rounded-md border-2 border-emerald-500/40">
          <img
            src={premiere_gif3}
            alt="Agendamento fácil"
            class="object-cover w-full h-full rounded-md"
          />
        </div>
        <!-- texto -->
        <div
          class="bg-gradient-to-t from-cyan-500/20 to-slate-900 border border-emerald-500/40 rounded-md p-6 flex flex-col justify-between"
        >
          <div class="flex justify-between items-center mb-4">
            <h3 class="text-3xl font-bold text-white">Agendamento Fácil</h3>
            <div class="bg-emerald-500 rounded-full p-2">
              <CalendarDays class="h-5 w-5 text-white" />
            </div>
          </div>
          <p class="text-gray-100 leading-relaxed mb-4">
            Reserve em segundos, sem complicação. Agende partidas, convide
            amigos e tenha total controle sobre seus horários.
          </p>
          <ul class="mt-auto text-gray-200 text-lg space-y-2">
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-cyan-400" strokeWidth={3} /> Reserva online
              rápida
            </li>
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-emerald-400" strokeWidth={3} /> Convite
              de jogadores direto no app
            </li>
            <li class="flex items-center gap-2">
              <Check class="h-7 w-7 text-cyan-400" strokeWidth={3} /> Notificações
              para lembrar dos jogos
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- CTA Section -->
  <section class="max-w-4xl mx-auto mb-20">
    <div
      class="bg-gradient-to-r from-emerald-600 to-cyan-600 rounded-2xl text-center flex items-center py-10 px-10 sm:py-0 sm:px-0"
    >
      <div class="sm:pl-10">
        <h2 class="text-3xl font-bold text-white mb-6">Pronto para começar?</h2>
        <p class="text-emerald-100 mb-6 max-w-2xl mx-auto text-lg">
          Junte-se à nossa comunidade e transforme a forma como você joga e
          gerencia esportes
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <button
            class="bg-white text-emerald-600 hover:bg-gray-100 px-4 py-3 rounded-lg text-sm"
            >Cadastrar Arena</button
          >
          <button
            class="px-4 py-3 rounded-lg border border-white text-white hover:bg-white hover:text-emerald-600 bg-transparent text-sm"
          >
            Encontrar Jogos
          </button>
        </div>
      </div>
      <img
        src={cta_img}
        alt="Jogador"
        class="hidden sm:block w-full max-h-96 object-cover"
      />
    </div>
  </section>

  <!-- Footer -->
  <footer class="container mx-auto px-4 py-12 border-t border-emerald-500/30">
    <div class="grid md:grid-cols-4 gap-8">
      <div>
        <div class="flex items-center gap-2 mb-4">
          <Crown class="h-6 w-6 text-cyan-400" />
          <span class="text-xl font-bold text-white">ArenaBook</span>
        </div>
        <p class="text-gray-400">
          Conectando jogadores e arenas para criar a melhor experiência
          esportiva.
        </p>
      </div>

      <div>
        <h4 class="text-white font-semibold mb-4">Produto</h4>
        <ul class="space-y-2 text-gray-400">
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors"
              >Recursos</a
            >
          </li>
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors">Preços</a>
          </li>
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors">API</a>
          </li>
        </ul>
      </div>

      <div>
        <h4 class="text-white font-semibold mb-4">Empresa</h4>
        <ul class="space-y-2 text-gray-400">
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors">Sobre</a>
          </li>
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors">Blog</a>
          </li>
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors"
              >Carreiras</a
            >
          </li>
        </ul>
      </div>

      <div>
        <h4 class="text-white font-semibold mb-4">Suporte</h4>
        <ul class="space-y-2 text-gray-400">
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors">Ajuda</a>
          </li>
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors">Contato</a
            >
          </li>
          <li>
            <a href="#" class="hover:text-cyan-400 transition-colors">Status</a>
          </li>
        </ul>
      </div>
    </div>

    <div
      class="border-t border-emerald-500/30 mt-8 pt-8 text-center text-gray-400"
    >
      <p>&copy; 2024 ArenaBook. Todos os direitos reservados.</p>
    </div>
  </footer>
</div>
