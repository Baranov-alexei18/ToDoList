<template>
  <div class="bar">ToDoList</div>
  <div class="grid">
    <div class="g-col-3" style="min-height: 85.4vh">1</div>
    <ListOrder class="g-col-5" />
    <div class="g-col-4" style="background: blue">2</div>

  </div>
</template>

<script>
import ListOrder from "./components/ListOrder.vue";

export default {
  name: "App",
  components: { ListOrder },

  data() {
    return {
      inputDate: "",
      inputMassiv: [],
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: #2c3e50;
}
.bar {
  font-size: 72px;
  background: -webkit-linear-gradient(#eee, #717bc8);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-align: center;
}
</style>
