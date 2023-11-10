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
    <hr>
    <div v-for="(work, idx) in inputMassiv" :key="idx">
      <div class="input-group mb-3">
        <div class="input-group-text">
          <input
            class="form-check-input mt-0"
            type="checkbox"
            value="what"
            aria-label="Checkbox for following text input"
          />
        </div>
        <input
          type="text"
          class="form-control"
          aria-label="Text input with checkbox"
          v-model="inputMassiv[idx]"
        />
        <button class="btn btn-danger" type="button" @click="deleteItems(idx)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},

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
    deleteItems(idx) {
      this.inputMassiv.splice(idx,1);
    },
  },
};
</script>

<style>
.input-text {
  padding-left: 20%;
  padding-right: 20%;
}
</style>