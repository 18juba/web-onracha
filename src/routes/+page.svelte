<script>
  import logo from "../lib/assets/img/on_racha_logo.png";
  import {
    CalendarDays,
    MapPin,
    Users,
    Crown,
    Play,
    Trophy,
  } from "@lucide/svelte";
  import dance_gif from "../lib/assets/img/artilheiro.gif";
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
      <button
        class="bg-cyan-500 hover:bg-cyan-600 text-white px-4 py-2 rounded-md cursor-pointer"
        >Entrar</button
      >
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
          <button
            class="flex items-center justify-center gap-2 bg-cyan-500 hover:bg-cyan-600 text-white px-8 py-3 rounded-lg cursor-pointer"
          >
            <Play class="h-5 w-5" />
            Começar Agora
          </button>
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
        incríveis
      </p>
    </div>

    <div class="grid md:grid-cols-3 gap-8">
      <!-- Card -->
      <div
        class="bg-gradient-to-t from-cyan-500/25 to-slate-800 border border-emerald-500/30 backdrop-blur-sm rounded-lg p-6"
      >
        <div class="bg-cyan-500 rounded-full p-3 w-fit mb-4">
          <MapPin class="h-6 w-6 text-white" />
        </div>
        <h3 class="text-xl font-bold text-white mb-3">Registro de Arenas</h3>
        <p class="text-gray-300">
          Proprietários podem cadastrar suas quadras com fotos, horários
          disponíveis e preços
        </p>
      </div>

      <div
        class="bg-gradient-to-t from-cyan-500/25 to-slate-800 border border-emerald-500/30 backdrop-blur-sm rounded-lg p-6"
      >
        <div class="bg-emerald-500 rounded-full p-3 w-fit mb-4">
          <CalendarDays class="h-6 w-6 text-white" />
        </div>
        <h3 class="text-xl font-bold text-white mb-3">Agendamento Fácil</h3>
        <p class="text-gray-300">
          Sistema intuitivo para reservar horários e organizar partidas com seus
          amigos
        </p>
      </div>

      <div
        class="bg-gradient-to-t from-cyan-500/25 to-slate-800 border border-emerald-500/30 backdrop-blur-sm rounded-lg p-6"
      >
        <div class="bg-cyan-500 rounded-full p-3 w-fit mb-4">
          <Users class="h-6 w-6 text-white" />
        </div>
        <h3 class="text-xl font-bold text-white mb-3">Comunidade Ativa</h3>
        <p class="text-gray-300">
          Conecte-se com outros jogadores, participe de jogos abertos e forme
          equipes
        </p>
      </div>
    </div>
  </section>

  <!-- About Section -->
  <section id="about" class="container mx-auto py-20">
    <div class="grid lg:grid-cols-2 gap-12 items-center">
      <div class="relative rounded-2xl border-2 border-emerald-500/30">
        <img
          src={dance_gif}
          alt="dancinha"
          class="object-cover w-full h-full rounded-2xl"
        />
      </div>

      <div class="space-y-6">
        <div class="flex items-start gap-4">
          <div class="bg-cyan-500 rounded-full p-2 mt-1">
            <Trophy class="h-4 w-4 text-white" />
          </div>
          <div>
            <h4 class="text-lg font-semibold text-white mb-2">
              Gestão Completa
            </h4>
            <p class="text-gray-300">
              Sistema completo para proprietários gerenciarem suas arenas
            </p>
          </div>
        </div>

        <div class="flex items-start gap-4">
          <div class="bg-emerald-500 rounded-full p-2 mt-1">
            <Users class="h-4 w-4 text-white" />
          </div>
          <div>
            <h4 class="text-lg font-semibold text-white mb-2">
              Comunidade Conectada
            </h4>
            <p class="text-gray-300">
              Jogadores podem encontrar partidas e formar grupos facilmente
            </p>
          </div>
        </div>

        <div class="flex items-start gap-4">
          <div class="bg-cyan-500 rounded-full p-2 mt-1">
            <CalendarDays class="h-4 w-4 text-white" />
          </div>
          <div>
            <h4 class="text-lg font-semibold text-white mb-2">
              Agendamento Inteligente
            </h4>
            <p class="text-gray-300">
              Calendário integrado com notificações e lembretes automáticos
            </p>
          </div>
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
