<template>
  <div id="burgerTable">
    <messageError v-show="msg" :msg="msg" :class="classError" />
    <div class="flex flex-col">
      <div class="overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="py-4 inline-block min-w-full sm:px-6 lg:px-8">
          <div class="overflow-hidden">
            <table class="min-w-full text-center">
              <thead class="border-b bg-gray-800">
                <tr>
                  <th
                    scope="col"
                    class="text-sm font-medium text-white px-6 py-4"
                  >
                    Pedido
                  </th>
                  <th
                    scope="col"
                    class="text-sm font-medium text-white px-6 py-4"
                  >
                    Cliente
                  </th>
                  <th
                    scope="col"
                    class="text-sm font-medium text-white px-6 py-4"
                  >
                    Pão:
                  </th>
                  <th
                    scope="col"
                    class="text-sm font-medium text-white px-6 py-4"
                  >
                    Carne:
                  </th>
                  <th
                    scope="col"
                    class="text-sm font-medium text-white px-6 py-4"
                  >
                    Opcionais:
                  </th>
                  <th
                    scope="col"
                    class="text-sm font-medium text-white px-6 py-4"
                  >
                    Ações:
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr
                  class="bg-white border-b"
                  v-for="burger in burgers"
                  :key="burger.id"
                >
                  <td
                    class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900"
                  >
                    {{ burger.id }}
                  </td>
                  <td
                    class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                  >
                    {{ burger.nome }}
                  </td>
                  <td
                    class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                  >
                    {{ burger.pao }}
                  </td>
                  <td
                    class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                  >
                    {{ burger.carne }}
                  </td>
                  <td
                    class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                  >
                    <ul>
                      <li
                        v-for="(opcional, index) in burger.opcionais"
                        :key="index"
                      >
                        {{ opcional.tipo }}
                      </li>
                    </ul>
                  </td>
                  <td
                    class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap"
                  >
                    <select
                      name="status"
                      class="form-select px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding bg-no-repeat border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                      @change="updatedBurger($event, burger.id)"
                    >
                      <option
                        v-for="stat in status"
                        :key="stat.id"
                        :value="stat.tipo"
                        :selected="burger.status == stat.tipo"
                      >
                        {{ stat.tipo }}
                      </option>
                    </select>
                    <button
                      class="deleteBtn ml-2 inline-block px-6 py-2.5 bg-red-600 text-white font-medium text-xs leading-tight uppercase rounded-full shadow-md hover:bg-red-700 hover:shadow-lg focus:bg-red-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-red-800 active:shadow-lg transition duration-150 ease-in-out"
                      @click="deleteBurger(burger.id)"
                    >
                      Cancelar
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import messageError from "./messageError.vue";

export default {
  name: "dashboardPedidos",
  components: { messageError },
  data() {
    return {
      burgers: null,
      burderId: null,
      status: [],
      msg: null,
      classError: null,
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");
      const data = await req.json();

      this.burgers = data;
      this.getStatus();
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();

      this.status = data;
    },
    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });
      const res = await req.json();

      this.msg = `Pedido ${id} deletado com sucesso!`;
      this.classError =
        "bg-indigo-100 rounded-lg py-5 px-6 mb-4 text-base text-indigo-700 mb-3 message-container";

      setTimeout(() => {
        this.msg = "";
      }, 3000);

      this.getPedidos();
    },
    async updatedBurger(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ status: option });

      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      this.msg = `Pedido nº ${id} foi atualizado para ${option}!`;
      this.classError =
        "bg-indigo-100 rounded-lg py-5 px-6 mb-4 text-base text-indigo-700 mb-3 message-container";

       setTimeout(() => {
        this.msg = "";
      }, 3000);

    },
  },
  mounted() {
    this.getPedidos();
  },
};
</script>

<style scoped>
#burgerTable {
  max-width: 1200px;
  margin: 0 auto;
}

#burgerTableHeading,
#burgerTableRows,
.burgerTableRow {
  display: flex;
  flex-wrap: wrap;
}

#burgerTableHeading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}
#burgerTableHeading div,
.burgerTableRow div {
  width: 19%;
}

.burgerTableRow {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}
</style>
