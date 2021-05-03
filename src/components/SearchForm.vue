<template>
  <div class="card">
    <form class="search-add-form">
      <input
        class="search-add-input input-style"
        :placeholder="placeholder"
        :value="modelValue"
        @input="inputEvent"
      />
      <span class="search-icon">🔎︎</span>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "SearchForm",
  props: {
    modelValue: {
      type: String,
    },
    placeholder: {
      type: String,
      required: false,
    },
  },
  setup(props, { emit }) {
    //Data
    const inputEvent = (event: any) => {
      emit("update:modelValue", event.target.value);
    };

    return { inputEvent };
  },
});
</script>

<style scoped>
.search-add-form {
  display: flex;
}
.search-add-input {
  position: relative;

  flex: 1;
  border-radius: unset;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}
.search-icon {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 8px;
  background: #ccc;
  color: white;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
}
</style>
