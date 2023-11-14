<template>
  <div class="bar">ToDoList</div>
  <div class="grid">
    <div class="g-col-3 checkList">
      <ListRoster
        :listRoster="listRoster"
        @addNewItemRoster="addNewItemRoster"
        @changeNameList="changeNameList"
      />
    </div>
    <ListOrder
      class="g-col-5"
      :listItemOrder="listOrderToWatch"
      @pushToList="pushToList"
      @deleteItems="deleteItems"
    />
    <div class="g-col-4 checkList"></div>
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
      inputDate: "",
      listOrderToWatch: [],
      inputMassiv: [],
      listRoster: [
        { id: 0, nameList: "1", listItems: ["adsf", "adf"] },
        {
          id: 1,
          nameList: "2",
          listItems: ["adsf1", "adf2", "dasf3"],
        },
        {
          id: 2,
          nameList: "3",
          listItems: ["adsf2", "adf2", "dasf3", "dsfasdf"],
        },
        {
          id: 3,
          nameList: "4",
          listItems: ["adsf2", "adf2", "dasf3", "dsfasdf"],
        },
      ],
    };
  },
  methods: {
    pushToList(inputDate) {
      this.listOrderToWatch.listItems.push(inputDate);
    },
    deleteItems(id){
      this.listOrderToWatch.listItems.splice(id, 1);
    },
    addNewItemRoster(obj) {
      this.listRoster.push({
        id: obj.id,
        nameList: obj.newNameItem,
        listItems: [],
      });
    },
    changeNameList(id) {
      this.listOrderToWatch = this.listRoster.find((el) => el.id === id);
    },
  },
  created() {
    if (this.listOrderToWatch)
      this.listOrderToWatch = this.listRoster.find((el) => el.id === 0);
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
