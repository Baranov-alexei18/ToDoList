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
        Поиск
      </button>
    </div>
    <hr />
    <div v-for="(order, id) in listRoster" :key="id">
      <div class="rosterOrder">
        {{ order.nameList }}
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
      inputSearch: "",
      newRosterItem: "",
      //listRoster: [[name: "Homework",listItem:["sdf","1"]],[name: "Sale",listItem:["fdsg","2"]]],
    };
  },
  methods: {
    addNewItemRoster() {
      if (this.newRosterItem) {
        console.log(this.listRoster);
        console.log(this.listRoster[2].nameList);
        //this.listRoster.push(this.newRosterItem)
        this.$emit("addNewItemRoster", this.newRosterItem)
    }
      this.newRosterItem = "";
    },
  },
  computed: {},
};
</script>
  
  <style>
.input-search {
  margin-top: 10px;
  padding-left: 10px;
  padding-right: 10px;
}
.rosterOrder {
  height: 30px;
  width: auto;
  margin-bottom: 3px;
  border-radius: 8px;
  background-color: black;
  color: white;
}
</style>