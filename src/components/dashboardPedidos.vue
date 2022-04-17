<template>
  <div id="burgerTable">
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
                <tr class="bg-white border-b">
                  <td
                    class="
                      px-6
                      py-4
                      whitespace-nowrap
                      text-sm
                      font-medium
                      text-gray-900
                    "
                  >
                    1
                  </td>
                  <td
                    class="
                      text-sm text-gray-900
                      font-light
                      px-6
                      py-4
                      whitespace-nowrap
                    "
                  >
                    Eduardo
                  </td>
                  <td
                    class="
                      text-sm text-gray-900
                      font-light
                      px-6
                      py-4
                      whitespace-nowrap
                    "
                  >
                    Integral
                  </td>
                  <td
                    class="
                      text-sm text-gray-900
                      font-light
                      px-6
                      py-4
                      whitespace-nowrap
                    "
                  >
                    Maminha
                  </td>
                  <td
                    class="
                      text-sm text-gray-900
                      font-light
                      px-6
                      py-4
                      whitespace-nowrap
                    "
                  >
                    <ul>
                      <li>Tomate</li>
                      <li>Salada</li>
                    </ul>
                  </td>
                  <td
                    class="
                      text-sm text-gray-900
                      font-light
                      px-6
                      py-4
                      whitespace-nowrap
                    "
                  >
                    <select name="status" class="status">
                      <option value="">Selecione o status do pedido!</option>
                    </select>
                    <button
                      class="
                        deleteBtn
                        ml-2
                        inline-block
                        px-6
                        py-2.5
                        bg-red-600
                        text-white
                        font-medium
                        text-xs
                        leading-tight
                        uppercase
                        rounded-full
                        shadow-md
                        hover:bg-red-700 hover:shadow-lg
                        focus:bg-red-700
                        focus:shadow-lg
                        focus:outline-none
                        focus:ring-0
                        active:bg-red-800 active:shadow-lg
                        transition
                        duration-150
                        ease-in-out
                      "
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
export default {};
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
