<template>
  <div class="bar">ToDoList</div>
  <div class="grid">
    <div class="g-col-3 checkList">
      <ListRoster
        :listRoster="listRoster"
        @addNewItemRoster="addNewItemRoster"
      />
    </div>
    <ListOrder class="g-col-5" />
    <div class="g-col-4" style="background: blue">2</div>
  </div>
</template>

<script>
import ListOrder from "./components/ListOrder.vue";
import ListRoster from "./components/ListRoster.vue";

export default {
  name: "App",
  components: { ListOrder, ListRoster },

  data() {
    return {
      IDBIndex: 1,
      inputDate: "",
      inputMassiv: [],
      listRoster: [
        { nameList: "1", listItems: ["adsf", "adf", "dasf"] },
        { nameList: "2", listItems: ["adsf1", "adf2", "dasf3"] },
        { nameList: "3", listItems: ["adsf2", "adf2", "dasf3"] },
      ],
    };
  },
  methods: {
    pushToList() {
      if (this.inputDate) this.inputMassiv.push(this.inputDate);
      this.inputDate = "";
    },
    addNewItemRoster(nameList) {
      this.listRoster.push({
        nameList: nameList,
        listItems: [],
      });
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
.checkList {
  padding: 5px;
  min-height: 85.4vh;
  background-color: whitesmoke;
  border-radius: 20px;
}
.bar {
  font-size: 72px;
  background: -webkit-linear-gradient(#eee, #717bc8);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-align: center;
}
</style>
