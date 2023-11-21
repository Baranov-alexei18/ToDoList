<template>
  <div>
    <div class="input-search input-group">
      <BaseInput v-model="inputSearch">
        <template v-slot:afterInput>
          <button
            class="btn btn-outline-secondary"
            type="button"
            id="button-addon2"
          >
            Search
          </button>
        </template>
      </BaseInput>
    </div>
    <hr />
    <div class="mx-2" v-for="(order, id) in listRoster" :key="id">
      <div
        :class="{ active: order.id === activeItem }"
        class="rosterOrder"
        @click="changeNameList(id)"
      >
        <label> {{ order.nameList }}</label>
      </div>
    </div>
    <div class="input-search">
      <BaseInput v-model="newRosterItem" @keydown.enter="addNewItemRoster">
        <template v-slot:afterInput>
          <button
            class="btn btn btn-primary"
            type="button"
            id="button-addon2"
            @click="addNewItemRoster"
          >
            Create
          </button>
        </template>
      </BaseInput>
    </div>
  </div>
</template>
  
  <script>
import BaseInput from "./ui/BaseInput.vue";

export default {
  components: { BaseInput },

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