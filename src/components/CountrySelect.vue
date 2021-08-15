<template>
  <div class="w-2/4 text-center m-auto">
    <select
      @change="onChange()"
      v-model="selected"
      class="form-select mt-2 border p-3 rounded"
    >
      <option value="0">Select Country</option>
      <option
        :key="country.ID"
        v-for="country in countries"
        :value="country.ID"
        >{{ country.Country }}</option
      >
    </select>
  </div>
</template>

<script>
export default {
  name: "CountrySelect",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected);
      this.$emit("get-country", country);
    },
  },
};
</script>
