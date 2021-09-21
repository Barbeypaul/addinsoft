<template>
  <div class="m-5">
    <div>
      <div>
        <GenererTab
          :genererTab="genererTab"
          :SupprimerTout="SupprimerTout"
        ></GenererTab>
      </div>
      <!-- Si le state Tableau est vide on affiche le component Alert -->
      <div v-if="tableau.table.length === 0">
        <Alert></Alert>
      </div>
      <!-- Si non on affiche le contenu du tableau -->
      <table v-else class="min-w-max w-full table-auto rounded-lg shadow-2xl">
        <thead class="">
          <tr class="bg-gray-200 bg-gray-800 uppercase text-sm leading-normal">
            <!-- On boucle sur les labels -->
            <th
              class="py-3 px-6 text-left text-white"
              v-for="label in tableau.labels"
              :key="label"
            >
              <!-- On affiche la valeur -->
              {{ label }}
            </th>
            <th class="py-3 px-6 text-left"></th>
          </tr>
        </thead>
        <tbody class="text-gray-600 text-sm font-light">
          <!-- On boucle sur le nombre de lignes dans le state tableau -->
          <tr
            class="border-b border-gray-200 hover:bg-gray-100"
            v-for="(array, index) in tableau.table"
            :key="array"
          >
            <!-- On boucle sur le contenu des lignes -->
            <td
              class="py-3 px-6 text-left whitespace-nowrap"
              v-for="item in array"
              :key="item"
            >
              <!-- On affiche l'item -->
              <div class="flex items-center">
                {{ item }}
              </div>
            </td>
            <td class="py-3 px-6 text-left whitespace-nowrap">
              <div class="flex items-center">
                <!-- Au clic supprimer une ligne avec comme paramètre l'index de la ligne -->
                <button class="text-red-500" @click="Supprimer(index)">
                  <i class="far fa-trash-alt"></i>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div>
      <!-- si le tableau est vide  -->
      <div v-if="tableau.table.length === 0"></div>
      <!-- si non on affiche le component GenererCsv  -->
      <GenererCsv v-else :genererCsv="genererCsv"></GenererCsv>
    </div>
  </div>
</template>

<script>
import GenererTab from "./GenererTab.vue";
import GenererCsv from "./GenererCsv.vue";
import Alert from "./Alerte.vue";
export default {
  components: {
    GenererTab,
    GenererCsv,
    Alert,
  },
  props: {
    msg: String,
  },
  data() {
    return {
      index: 0,
      tableau: {
        labels: [],
        table: [],
      },
    };
  },
  methods: {
    /**
     * Générer le tableau
     * parm : nombre de lignes
     * parm : nombre de colonnes
     *
     */
    genererTab: function (col, row) {
      this.tableau.labels = [];
      this.tableau.table = [];
      for (let irow = 0; irow < row; irow++) {
        const tab = [];
        for (let icol = 0; icol < col; icol++) {
          tab.push(Math.random().toFixed(3));
        }
        this.tableau.table.push(tab);
      }
      for (let icol = 0; icol < col; icol++) {
        this.tableau.labels.push("X" + icol);
      }
    },
    /**
     * Supprimer une ligne
     * index : ligne a supprimer
     */
    Supprimer: function (index) {
      this.index = index;
      return this.tableau.table.splice(index, 1);
    },
    /**
     * Supprimer le contenu du tableau
     */
    SupprimerTout: function () {
      this.tableau.table = [];
      this.tableau.labels = [];
    },
    /**
     * Génerer un fichier Csv en envoyant le tableau a l'api
     */
    genererCsv: async function () {
      const table = {
        labels: ["X1", "X2"],
        table: [
          ["0.689", "-0.837"],
          ["0.181", "0.880"],
          ["0.938", "3.239"],
          ["-0.039", "1.193"],
          ["0.449", "1.975"],
          ["0.087", "-0.701"],
          ["1.290", "-0.809"],
          ["1.025", "0.772"],
          ["-0.732", "0.979"],
        ],
      };
      const requestOptions = {
        method: "POST",
        mode: "cors",
        headers: {
          "Content-Type": "application/json",
          "Access-Control-Allow-Origin": "https://localhost:8080/",
          accept: "text/plain",
          "Cache-Control": null,
          "X-Requested-With": null,
        },
        body: table,
      };
      const response = await fetch(
        "http://readytorun.azurewebsites.net/api/CSV",
        requestOptions
      );
      console.log(response);

      const data = await response.json();
      this.postId = data.id;
    },
  },
};
</script>

