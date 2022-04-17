<template>
  <div>
    <messageError v-show="msg" :msg="msg" :class="classError"/>
    <hr class="mt-5 border-2 bg-black" />
    <form @submit="createBurger($event)" id="burgerForm">
      <label
        for="nome"
        class="
          block
          border-l-8 border-l-indigo-500
          w-full
          text-left
          mt-5
          text-lg
          font-medium
          text-gray-900
          dark:text-black
        "
        >Nome do cliente</label
      >
      <input
        type="text"
        id="nome"
        class="
          bg-gray-50
          border border-gray-300
          text-gray-900
          rounded-lg
          text-lg
          focus:ring-blue-500 focus:border-blue-500
          w-full
          p-2.5
          dark:bg-gray-700
          dark:border-gray-600
          dark:placeholder-gray-400
          dark:text-white
          dark:focus:ring-blue-500
          dark:focus:border-blue-500
        "
        placeholder="Digite o nome do cliente"
        v-model="nome"
      />
      <label
        for="paes"
        class="
          block
          border-l-8 border-l-indigo-500
          w-full
          text-left
          mt-2
          text-lg
          font-medium
          text-black
          dark:text-black
        "
        >Selecione o pão</label
      >
      <select
        id="paes"
        class="
          bg-gray-50
          w-full
          border border-gray-300
          text-gray-900
          rounded-lg
          focus:ring-blue-500 focus:border-blue-500
          text-lg
          p-2.5
          dark:bg-gray-700
          dark:border-gray-600
          dark:placeholder-gray-400
          dark:text-white
          dark:focus:ring-blue-500
          dark:focus:border-blue-500
        "
        v-model="pao"
      >
        <option value="">Selecione o seu pão</option>
        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
          {{ pao.tipo }}
        </option>
      </select>

      <label
        for="carnes"
        class="
          border-l-8 border-l-indigo-500
          block
          w-full
          text-left
          mt-2
          text-lg
          font-medium
          text-gray-900
          dark:text-black
        "
        >Selecione a carne do seu Burger:</label
      >
      <select
        id="carnes"
        class="
          bg-gray-50
          w-full
          border border-gray-300
          text-gray-900 text-lg
          rounded-lg
          focus:ring-blue-500 focus:border-blue-500
          p-2.5
          dark:bg-gray-700
          dark:border-gray-600
          dark:placeholder-gray-400
          dark:text-white
          dark:focus:ring-blue-500
          dark:focus:border-blue-500
        "
        v-model="carne"
      >
        <option value="">Selecione o tipo de carne</option>
        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
          {{ carne.tipo }}
        </option>
      </select>

      <label
        for="opcionais"
        class="
          border-l-8 border-l-indigo-500
          block
          mt-2
          w-full
          text-left text-lg
          font-medium
          text-gray-900
          dark:text-black
        "
        >Selecione os opcionais do seu Burger:</label
      >
      <fieldset class="checks form-check">
        <div
          class="mt-3 text-lg rounded inline-block mb-4"
          v-for="opcional in opcionaisdata"
          :key="opcional.id"
        >
          <input
            :id="opcional.id"
            type="checkbox"
            class="
              ml-2
              form-check-input
              appearance-none
              h-4
              w-4
              border border-gray-300
              rounded-sm
              bg-white
              checked:bg-green-600 checked:green-blue-600
              focus:outline-none
              transition
              duration-200
              mt-1
              align-top
              bg-no-repeat bg-center bg-contain
              float-left
              mr-2
              cursor-pointer
            "
            v-model="opcionais"
            :value="opcional"
          />
          <label
            :for="opcional.id"
            class="text-lg text-gray-900 dark:text-gray-900"
            >{{ opcional.tipo }}</label
          >
        </div>
      </fieldset>
      <button
        type="submit"
        class="
          text-white
          bg-gradient-to-br
          from-purple-600
          to-blue-500
          hover:bg-gradient-to-bl
          focus:ring-4 focus:outline-none focus:ring-blue-300
          dark:focus:ring-blue-800
          font-medium
          rounded-lg
          text-sm
          px-5
          py-2.5
          text-center
          mr-2
          mb-2
        "
      >
        Enviar Pedido
      </button>
    </form>
  </div>
</template>

<script>
import messageError from './messageError.vue'

export default {
  name: "burgerForm",
  components:{messageError},
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcional: null,
      opcionais: [],
      msg: null,
  
      classError: null,
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },
    async createBurger(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        carne: this.carne,
        pao: this.pao,
        opcionais: Array.from(this.opcionais),
        status: "solicitado",
      };
      const dataJson = JSON.stringify(data);
      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "content-type": "application/json" },
        body: dataJson,
      });
      const res = await req.json();
      this.limparCampos();
      this.msg = `Pedido ${res.id} realizado com sucesso!`;
      this.classError = 'bg-green-100 rounded-lg py-5 px-6 mb-4 text-base text-green-700 mb-3 message-container'

      setTimeout(() =>{
        this.msg = '';
      }, 3000)

    },
    limparCampos(){
      this.nome = '';
      this.carne = '';
      this.pao = '';
      this.opcionais = '';
    },
    
  },
  mounted() {
    this.getIngredients();
  },
};
</script>
<style scoped>
#burgerForm {
  max-width: 450px;
  margin: 0 auto;
}
.checks {
  max-width: 450px;
}
</style>