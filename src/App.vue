<template>
  <div class="bar">ToDoList</div>
  <div class="container-md">
    <div class="row" style="gap: 5px">
      <div class="d-none d-sm-flex col-sm-3 mx-2 checkList">
        <ListRoster
          :listRoster="listRoster"
          @addNewItemRoster="addNewItemRoster"
          @changeNameList="changeNameList"
        />
      </div>
      <ListOrder
        class="col checkList"
        :listItemOrder="listOrderToWatch"
        @pushToList="pushToList"
        @deleteItems="deleteItems"
        @deleteItemsComplitied="deleteItemsComplitied"
        @taskComplitied="taskComplitied"
        @returnTask="returnTask"
      />
    </div>
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
      listOrderToWatch: [],
      listRoster: [
        {
          id: 0,
          nameList: "Заметки",
          listItems: [
            { nameItem: "Удобное приложение", complitied: false },
            { nameItem: "Красивый интерфейс", complitied: false },
            { nameItem: "Красивые кнопочки Bootstrap", complitied: false },
          ],
          arrayComplitied: [],
        },
        {
          id: 1,
          nameList: "Домашние дела",
          listItems: [
            { nameItem: "Убрать на стол", complitied: false },
            { nameItem: "Помыть посуду", complitied: false },
            { nameItem: "Пропылесосить", complitied: false },
            { nameItem: "Протереть пыль", complitied: false },
          ],
          arrayComplitied: [],
        },
      ],
    };
  },
  methods: {
    pushToList(inputDate) {
      this.listOrderToWatch.listItems.push({
        nameItem: inputDate,
        complitied: false,
      });
    },
    deleteItems(id) {
      this.listOrderToWatch.listItems.splice(id, 1);
    },
    deleteItemsComplitied(id) {
      this.listOrderToWatch.arrayComplitied.splice(id, 1);
    },
    addNewItemRoster(obj) {
      this.listRoster.push({
        id: obj.id,
        nameList: obj.newNameItem,
        listItems: [
          {
            nameItem: "",
            complitied: false,
          },
        ],
        arrayComplitied: [],
      });
    },
    changeNameList(id) {
      this.listOrderToWatch = this.listRoster.find((el) => el.id === id);
    },
    taskComplitied(itemComplitied) {
      this.listOrderToWatch.arrayComplitied.push(itemComplitied);
    },
    returnTask(itemTask) {
      this.listOrderToWatch.listItems.push(itemTask);
    },
  },
  created() {
    if (this.listOrderToWatch)
      this.listOrderToWatch = this.listRoster[0];
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
@media (max-width: 576px){
  .bar {
    font-size: 48px;
  }
}
</style>