<template>
  <div class="container">
    <edit-form
        :value="itemToEdit.value"
        :name="itemToEdit.name"
        @updateItem="updateItemValue"
        @cancelEdit="clearItemToEdit"
    ></edit-form>

    <div class="card p-4 shadow-lg" style="height: 520px">
      <ul class="overflow-y-scroll">
        <li v-for="item of data" :key="item.name" @click="handleItemEdit(item)">
          <div
              class="card my-1"
              :class="{ item: true, item__active: isItemActive(item.name) }"
          >
            <div class="card-body p-2">
              {{ item.name + ": " + item.value }}
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import EditForm from "@/components/editForm";
export default {
  name: "App",
  components: { EditForm },
  data() {
    return {
      data: [],
      itemToEdit: { name: "", value: "" },
    };
  },

  created() {
    this.data = this.fillingArray();
  },

  methods: {
    clearItemToEdit() {
      this.itemToEdit = { name: "", value: "" };
    },

    fillingArray() {
      const createItem = (number) => ({
        name: `foo${number + 1}`,
        value: `bar${number + 1}`,
      });

      return new Array(40).fill(null).map((_, idx) => createItem(idx));
    },

    handleItemEdit(item) {
      this.itemToEdit = item;
    },

    updateItemValue(value) {
      const idx = this.data.findIndex((e) => e.name === this.itemToEdit.name);

      this.data[idx].value = value;

      this.clearItemToEdit();
    },

    isItemActive(name) {
      return this.itemToEdit.name === name;
    },
  },
};
</script>

<style src="../src/assets/css/test-array.css" />
