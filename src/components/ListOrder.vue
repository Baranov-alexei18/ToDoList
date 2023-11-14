<template>
  <div>
    <div class="input-text input-group mb-3">
      <input
        type="text"
        class="form-control"
        placeholder="any"
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
        v-model="inputDate"
        @keydown.enter="pushToList()"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
        @click="pushToList()"
      >
        +
      </button>
    </div>
    <hr />
    <div v-for="(item, idx) in listItemOrder.listItems" :key="idx">
      <div
        class="input-group mb-3"
        v-if="item.nameItem "
        :style="item.complitied ? 'opacity: 50%' : 'opacity: 100%'">
        <div class="input-group-text">
          <input
            class="form-check-input mt-0"
            type="checkbox"
            v-model="item.complitied"
            aria-label="Checkbox for following text input"
          />
        </div>
        <input
          type="text"
          class="form-control"
          :class="item.complitied ? 'form-compile' : 'form-control'"
          aria-label="Text input with checkbox"
          v-model="item.nameItem"
        />
        <button class="btn btn-danger" type="button" @click="deleteItems(idx)">
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},

  props: {
    listItemOrder: {
      type: Object,
    },
  },

  data() {
    return {
      inputDate: "",
    };
  },
  methods: {
    pushToList() {
      if (this.inputDate) this.$emit("pushToList", this.inputDate);
      this.inputDate = "";
    },
    deleteItems(idx) {
      this.$emit("deleteItems", idx);
    },
  },
};
</script>

<style>
.input-text {
  padding-left: 10%;
  padding-right: 10%;
}
.form-compile {
  opacity: 80%;
  text-decoration: line-through;
  width: auto;
}
</style>