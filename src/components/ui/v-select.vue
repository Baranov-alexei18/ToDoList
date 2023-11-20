<template>
  <select
    class="form-select form-select-lg"
    aria-label="Large select example"
    v-model="activeItem"
  >
    <option v-for="(order, id) in listRoster" :key="id" :value="id">
      {{ order.nameList }}
    </option>
  </select>
</template>

<script>
export default {
  name: "v-select",
  props: ["listRoster"],

  data() {
    return {
      activeItem: 0,
    };
  },
  methods: {
    changeNameList() {
      const id = 0;
      this.$emit("changeNameList", id);
    },
  },
  watch: {
    activeItem: function (id) {
        this.$emit("changeNameList", id);
    },
  }
};

// this won't work because we are passing a number to watch()

</script>

<style>
</style>