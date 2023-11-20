<template>
  <div>
    <div class="input-search input-group">
      <input
        type="text"
        class="form-control"
        placeholder="Поиск"
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
        v-model="inputSearch"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
      >
        Search
      </button>
    </div>
    <hr />
    <div class="listItem" v-for="(order, id) in listRoster" :key="id">
      <div
        :class="{ active: order.id === activeItem }"
        class="rosterOrder"
        @click="changeNameList(id)"
      >
        <label> {{ order.nameList }}</label>
      </div>
    </div>

    <div class="input-search input-group">
      <input
        type="text"
        class="form-control"
        placeholder=""
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
        v-model="newRosterItem"
        @keydown.enter="addNewItemRoster"
      />
      <button
        class="btn btn btn-primary"
        type="button"
        id="button-addon2"
        @click="addNewItemRoster"
      >
        Create
      </button>
    </div>
  </div>
</template>
  
  <script>
export default {
  components: {},

  props: ["listRoster"],
  data() {
    return {
      activeItem: 0,
      inputSearch: "",
      newRosterItem: "",
    };
  },
  methods: {
    addNewItemRoster() {
      if (this.newRosterItem) {
        this.$emit("addNewItemRoster", {
          id: this.listRoster.length,
          newNameItem: this.newRosterItem,
        });
      }
      this.newRosterItem = "";
    },
    changeNameList(id) {
      this.activeItem = id;
      this.$emit("changeNameList", id);
    },
  },

  computed: {},
};
</script>
  
  <style>
.listItem {
  margin-left: 10px;
  margin-right: 10px;
}
.input-search {
  margin-top: 10px;
  padding-left: 10px;
  padding-right: 10px;
}
.rosterOrder {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 30px;
  width: auto;
  margin-bottom: 3px;
  border-radius: 8px;
  background-color: black;
  color: white;
}
.active {
  background-color: blue;
}
</style>