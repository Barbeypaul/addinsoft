<template>
  <div class="flex flex-row mt-5 mb-5 flex items-center">
    <p class="text-gray-600 m-1 font-semibold text-md">Row :</p>
    <div class="custom-number-input h-10 w-32 mr-5">
      <div
        class="
          flex flex-row
          h-10
          w-full
          rounded-lg
          relative
          bg-transparent
          shadow-2xl
        "
      >
        <!-- Au clic on exécute la fonction moinsRow -->
        <button
          @click="moinsRow()"
          class="
            bg-white
            text-gray-600
            hover:text-gray-700
            hover:bg-gray-200
            h-full
            w-20
            rounded-l
            cursor-pointer
            outline-none
          "
        >
          <span class="m-auto text-2xl font-thin">−</span>
        </button>
        <input
          v-model="row"
          type="number"
          class="
            outline-none
            focus:outline-none
            text-center
            w-full
            bg-white
            font-semibold
            text-md
            hover:text-black
            focus:text-black
            md:text-basecursor-default
            flex
            items-center
            text-gray-700
            outline-none
          "
          name="custom-input-number"
        />
        <!-- Au clic on exécute  la fonction plusRow -->
        <button
          @click="plusRow()"
          class="
            bg-white
            text-gray-600
            hover:text-gray-700
            hover:bg-gray-200
            h-full
            w-20
            rounded-r
            cursor-pointer
          "
        >
          <span class="m-auto text-2xl font-thin">+</span>
        </button>
      </div>
    </div>
    <p class="text-gray-600 m-1 font-semibold text-md">Col :</p>
    <div class="custom-number-input h-10 w-32 mr-5">
      <div
        class="
          flex flex-row
          h-10
          w-full
          rounded-lg
          relative
          bg-transparent
          shadow-2xl
        "
      >
        <!-- Au clic on exécute  la fonction moinsCol -->
        <button
          @click="moinsCol()"
          class="
            bg-white
            text-gray-600
            hover:text-gray-700
            hover:bg-gray-200
            h-full
            w-20
            rounded-l
            cursor-pointer
            outline-none
          "
        >
          <span class="m-auto text-2xl font-thin">−</span>
        </button>
        <input
          v-model="col"
          type="number"
          class="
            outline-none
            focus:outline-none
            text-center
            w-full
            bg-white
            font-semibold
            text-md
            hover:text-black
            focus:text-black
            md:text-basecursor-default
            flex
            items-center
            text-gray-700
            outline-none
          "
          name="custom-input-number"
        />
        <!-- Au clic on exécute  la fonction plusCol -->
        <button
          @click="plusCol()"
          class="
            bg-white
            text-gray-600
            hover:text-gray-700
            hover:bg-gray-200
            h-full
            w-20
            rounded-r
            cursor-pointer
          "
        >
          <span class="m-auto text-2xl font-thin">+</span>
        </button>
      </div>
    </div>
    <!-- On bloque le bouton si col et row sont égal a 0-->
    <button
      class="
        h-10
        w-32
        mr-5
        bg-white
        text-gray-700
        font-bold
        rounded
        opacity-50
        cursor-not-allowed
        shadow-2xl
      "
      v-if="col === 0 || row === 0"
    >
      Générer
      <i class="fas fa-table"></i>
    </button>
    <!-- si non -->
    <button
      class="
        h-10
        w-32
        mr-5
        bg-white
        hover:bg-gray-200
        text-gray-700
        font-bold
        rounded
        shadow-2xl
      "
      v-else
      @click="genererTab(col, row)"
    >
      Générer
      <i class="fas fa-table"></i>
    </button>
    <!--  si col et row sont égal a 0-->

    <div v-if="col === 0 || row === 0"></div>
    <!--  si non  on affiche le bouton Supprimer-->
    <!-- Au clic on exécute la fonction SupprimerTabColRow -->
    <button
      v-else
      class="
        h-10
        pl-3
        pr-3
        mr-5
        bg-white
        hover:bg-gray-200
        text-red-500
        font-bold
        rounded
      "
      @click="SupprimerTabColRow"
    >
      Tout supprimer
      <i class="far fa-trash-alt"></i>
    </button>
  </div>
</template>

<script>
export default {
  /**
   * props : Founction pour génerer le tableau
   * props : Founction pour Supprimer le tableau
   */
  props: {
    genererTab: { type: Function },
    SupprimerTout: { type: Function },
  },
  /**
   * state col : conteur nombre de colonnes
   * state row : conteur nombre de lignes
   */
  data() {
    return {
      col: 0,
      row: 0,
    };
  },
  methods: {
    // Fonctions pour incrémenter et décrémenter les conteurs col et row
    plusRow() {
      if (this.row <= 14) {
        return this.row++;
      }
    },
    moinsRow() {
      if (this.row >= 1) {
        this.row--;
      }
    },
    plusCol() {
      if (this.col <= 14) {
        this.col++;
      }
    },
    moinsCol() {
      if (this.col >= 1) {
        this.col--;
      }
    },
    /**
     * Supprimer contenu du tableau
     * On exécute la fonction props SupprimerTout
     */
    SupprimerTabColRow() {
      this.col = 0;
      this.row = 0;
      this.SupprimerTout();
    },
  },
};
</script>


<style scoped>
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.custom-number-input input:focus {
  outline: none !important;
}

.custom-number-input button:focus {
  outline: none !important;
}
</style>