<script>
</script>

<div
  class="relative min-w-screen min-h-screen flex-1 flex flex-col justify-center items-center"
>
  <div class="fixed w-4xl h-7/12 backdrop-blur-sm">
    <!-- Lado Esquerdo -->
    <div
      class="absolute left-0 h-full w-4/12 flex flex-col justify-between items-center
        rounded-2xl border-2 border-gray-400/50 px-6 py-10"
    >
      <img
        class="w-full h-3/12 object-contain"
        src="https://www.central3.com.br/wp-content/uploads/2017/03/brasao-copa-nordeste.png"
        alt="Copa do Nordeste"
      />

      <div
        class="w-full h-3/12 flex flex-col justify-between items-center text-white text-balance"
      >
        <h1 class="text-xl font-bold">
          Cadastre-se
          <p class="text-sm text-white/60">Ou faça login para continuar</p>
        </h1>
      </div>

      <button
        class="w-52 h-14 flex justify-center items-center rounded-4xl border-2 border-white
          cursor-pointer transition-all duration-300 hover:bg-green-600/5 hover:border-green-500"
      >
        <p
          class="flex justify-center items-center w-full h-full text-base
            font-bold text-white transition-all duration-300 hover:text-green-500"
        >
          Fazer Login
        </p>
      </button>
    </div>

    <!-- Lado Direito -->
    <div
      class="absolute right-0 top-[18px] h-11/12 w-8/12 flex flex-col justify-start items-start
        rounded-r-2xl border-2 border-gray-400/50 border-l-0"
    >
      <h1 class="text-2xl font-bold text-white">Cadastro</h1>

      <div class="w-full h-4 flex justify-center gap-2 items-center">
        <hr class="w-3/12 h-0.5 bg-white" />
        <p class="text-white text-xs font-bold">Cadastre-se usando seu email</p>
        <hr class="w-3/12 h-0.5 bg-white" />
      </div>

      <div class="w-full h-52 flex flex-col justify-center items-center gap-3">
        <input
          type="text"
          placeholder="Nome"
          class="w-full h-10 rounded-4xl border-2 border-gray-400/50
            px-4 py-2 text-base font-bold text-white
            transition-all duration-300 hover:bg-green-600/5 hover:border-green-500 active:bg-green-600/5"
        />
        <input
          type="email"
          placeholder="Email"
          class="w-full h-10 rounded-4xl border-2 border-gray-400/50
            px-4 py-2 text-base font-bold text-white
            transition-all duration-300 hover:bg-green-600/5 hover:border-green-500 active:bg-green-600/5"
        />
        <input
          type="password"
          placeholder="Senha"
          class="w-full h-10 rounded-4xl border-2 border-gray-400/50
            px-4 py-2 text-base font-bold text-white
            transition-all duration-300 hover:bg-green-600/5 hover:border-green-500 active:bg-green-600/5"
        />
        <input
          type="password"
          placeholder="Confirmar Senha"
          class="w-full h-10 rounded-4xl border-2 border-gray-400/50
            px-4 py-2 text-base font-bold text-white
            transition-all duration-300 hover:bg-green-600/5 hover:border-green-500 active:bg-green-600/5"
        />
      </div>
    </div>
  </div>
</div>
