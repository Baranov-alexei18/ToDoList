<template>
  <ListOrder />
</template>

<script>


import ListOrder from "./components/ListOrder.vue";

export default {
  name: "App",
  components: { ListOrder },

  data() {
    return {
      inputDate: "",
      inputMassiv: ["Home work", "homeTask"],
    };
  },
  methods: {
    pushToList() {
      if (this.inputDate) this.inputMassiv.push(this.inputDate);
      this.inputDate = "";
    },
  },
};
</script>

<style>
@import '~bootstrap/dist/css/bootstrap.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
