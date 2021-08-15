<template>
  <div class="grid md:grid-cols-2 gap-3">
    <!-- CASES -->
    <div class="shadow-md bg-indigo-200 p-10 text-center rounded">
      <h3 class="text-3xl text-indigo-800 font-bold mb-4">
        CASES
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New Cases:</span>
        {{ comma(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total Cases:</span>
        {{ comma(stats.TotalConfirmed) }}
      </div>
    </div>

    <!-- DEATHS -->
    <div class="shadow-md bg-indigo-200 p-10 text-center rounded">
      <h3 class="text-3xl text-indigo-800 font-bold mb-4">
        DEATHS
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New Deaths:</span>
        {{ comma(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total Deaths:</span>
        {{ comma(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DataBoxes",
  props: ["stats"],
  methods: {
    comma(n) {
      return n.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>
