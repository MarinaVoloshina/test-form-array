<template>
  <form @submit.prevent="updateItemValue">
    <div class="card my-2 mt-4 p-4 shadow-lg">
      <label for="itemInput" class="form-label">
        {{
          name ? "Edit the " + name + " value:" : "Select item to edit"
        }}</label
      >
      <input
        class="form-control"
        name="itemInput"
        type="text"
        :placeholder="!name ? 'Item value' : name"
        v-model="itemValue"
        :disabled="isFormDisabled"
        ref="itemInput"
      />

      <div class="d-grid gap-3 d-sm-flex pt-2">
        <button
          type="submit"
          class="btn btn-outline-secondary btn-sm"
          :disabled="isFormDisabled"
        >
          Ok
        </button>

        <button
          type="button"
          class="btn btn-light btn-sm"
          @click="cancelEdit"
          :disabled="isFormDisabled"
        >
          Cancel
        </button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "editForm",
  emits: ["updateItem", "cancelEdit"],
  props: {
    name: String,
    value: String,
  },
  computed: {
    isFormDisabled() {
      return !this.name;
    },
  },
  data() {
    return {
      itemValue: "",
    };
  },
  methods: {
    updateItemValue() {
      this.$emit("updateItem", this.itemValue);
    },
    cancelEdit() {
      this.$emit("cancelEdit");
    },
  },
  watch: {
    name(newVal) {
      if (newVal) {
        this.$nextTick(() => this.$refs.itemInput.focus());
      }
    },
    value(newValue) {
      this.itemValue = newValue;
    },
  },
};
</script>
