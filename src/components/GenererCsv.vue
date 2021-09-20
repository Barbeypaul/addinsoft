<template>
  <div>
    <button
      @click="genererCsv()"
      class="
        mt-5
        bg-gray-300
        hover:bg-gray-400
        text-gray-800
        font-bold
        py-2
        px-4
        rounded
        inline-flex
        items-center
        shadow-2xl
      "
    >
      <i class="fas fa-file-csv text-black"></i>

      <span>Download</span>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    genererCsv: { type: Function },
  },
};
</script>