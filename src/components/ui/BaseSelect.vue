<template>
  <div>
    <div class="input-search-lg input-group mb-1">
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
    <select
      class="form-select form-select-lg"
      aria-label="Large select example"
      v-model="activeItem"
    >
      <option v-for="(order, id) in listRoster" :key="id" :value="id">
        {{ order.nameList }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "v-select",
  props: ["listRoster"],

  data() {
    return {
      activeItem: 0,
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
  },
  watch: {
    activeItem: function (id) {
      this.$emit("changeNameList", id);
    },
  },
};

// this won't work because we are passing a number to watch()
</script>

<style>
</style>