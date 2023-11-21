<template>
  <div class="checkList">
    <BaseInput class="mt-2" v-model="inputDate" @keydown.enter="pushToList()">
      <template v-slot:afterInput>
        <button
          class="btn btn-outline-secondary"
          type="button"
          id="button-addon2"
          @click="pushToList()"
        >
          +
        </button>
      </template>
    </BaseInput>
    <hr />
    <div v-for="(item, idx) in listItemOrder.listItems" :key="idx">
      <div
        class="input-group mb-3"
        v-if="item.nameItem"
        :style="item.complitied ? 'opacity: 50%' : 'opacity: 100%'"
        @dragstart="startDrag($event, idx)"
        @drop="onDrop($event, listItemOrder.listItems, idx)"
        :draggable="true"
        @dragover.prevent
        @dragenter.prevent
      >
        <BaseInput
          :class="item.complitied ? 'form-compile' : 'form-control'"
          v-model="item.nameItem"
        >
          <template v-slot:beforeInput>
            <div style="width: 30px; margin-top: 6px">
              <img src="../assets/list.png" alt="adsf" />
            </div>
            <div class="input-group-text">
              <input
                class="form-check-input mt-0"
                type="checkbox"
                v-model="item.complitied"
                aria-label="Checkbox for following text input"
                @change="taskComplitied(listItemOrder, idx)"
              />
            </div>
          </template>
          <template v-slot:afterInput>
            <button
              class="btn btn-danger"
              type="button"
              @click="deleteItems(idx)"
            >
              Delete
            </button>
          </template>
        </BaseInput>
      </div>
    </div>
    <div v-if="listItemOrder.arrayComplitied.length">
      <div class="chip">
        <p style="margin: 0">
          Выполнено: {{ listItemOrder.arrayComplitied.length }}
        </p>
      </div>
      <div v-for="(item, idx) in listItemOrder.arrayComplitied" :key="idx">
        <BaseInput 
          :class="item.complitied ? 'form-compile' : 'form-control'"
          v-model="item.nameItem"
          class="input-group mb-3"
          v-if="item.nameItem"
          :style="item.complitied ? 'opacity: 50%' : 'opacity: 100%'"
        >
          <template v-slot:beforeInput>
            <div style="width: 30px; margin-top: 6px">
              <img src="../assets/list.png" alt="adsf" />
            </div>
            <div class="input-group-text">
              <input
                class="form-check-input mt-0"
                type="checkbox"
                v-model="item.complitied"
                aria-label="Checkbox for following text input"
                @change="returnTask(listItemOrder, idx)"
              />
            </div>
          </template>
          <template v-slot:afterInput>
            <button
              class="btn btn-danger"
              type="button"
              @click="deleteItemsComplitied(idx)"
            >
              Delete
            </button>
          </template>
        </BaseInput>
      </div>
    </div>
  </div>
</template>

<script>
import { useToast } from "vue-toast-notification";
import "vue-toast-notification/dist/theme-sugar.css";

import BaseInput from "./ui/BaseInput.vue";

export default {
  components: { BaseInput },

  props: {
    listItemOrder: {
      type: Object,
    },
  },

  data() {
    return {
      dragOnDrop: null,
      inputDate: "",
      oldInputDate: false,
      arrayComplitied: [],
    };
  },

  methods: {
    pushToList() {
      const toast = useToast();
      const oldInputDate = this.listItemOrder.listItems.some(
        (item) => item.nameItem === this.inputDate
      );

      if (!this.inputDate.length) {
        toast.error("This task is empty");
      } else if (oldInputDate) {
        toast.error("This task already created");
      } else if (this.inputDate && !oldInputDate) {
        this.$emit("pushToList", this.inputDate);
        toast.success("New task added");
        this.inputDate = "";
      }
    },
    deleteItems(idx) {
      this.$emit("deleteItems", idx);
    },
    deleteItemsComplitied(idx) {
      this.$emit("deleteItemsComplitied", idx);
    },
    startDrag(evt, id) {
      evt.dataTransfer.dropEffect = "move";
      evt.dataTransfer.effectAllowed = "move";
      this.dragOnDrop = id;
    },
    onDrop(evt, list, id) {
      const container = list.splice(this.dragOnDrop, 1)[0];
      list.splice(id, 0, container);
      this.dragOnDrop = null;
    },
    taskComplitied(list, id) {
      // eslint-disable-next-line no-constant-condition
      if ((list.listItems[id].complitied = true)) {
        const container = list.listItems.find(
          (item) => item.nameItem === list.listItems[id].nameItem
        );
        this.deleteItems(id);
        this.$emit("taskComplitied", container);
      }
    },
    returnTask(list, id) {
      const container = list.arrayComplitied.find(
        (item) => item.nameItem === list.arrayComplitied[id].nameItem
      );
      this.deleteItemsComplitied(id);
      this.$emit("returnTask", container);
    },
  },

  computed: {},
  watch: {},
};
</script>

<style>
.checkList {
  padding: 5px;
  min-height: 85.4vh;
  background-color: whitesmoke;
  border-radius: 20px;
}
.form-compile input{
  opacity: 80%;
  text-decoration: line-through;
}
.chip {
  margin-bottom: 3px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 110px;
  height: 30px;
  font-size: 15px;
  background-color: antiquewhite;
  border-radius: 10px;
}
@media (max-width: 576px) {
  .checkList {
    margin-left: 10px;
    margin-right: 10px;
  }
}
</style>