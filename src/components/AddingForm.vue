<template>
  <div class="add-item-container card">
    <div class="add-item-form-header">Adding form</div>
    <input v-model.trim="data.title" placeholder="Title" class="input-style" />
    <textarea
      v-model.trim="data.description"
      placeholder="Description"
      class="input-style"
    ></textarea>
    <button class="add-item-btn" type="button" @click="addItemFun">
      + Add Item
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import { Item } from "@/Interfaces/Item";

export default defineComponent({
  name: "AddingForm",
  setup(props, { emit }) {
    let lastNumber = 1;
    const data = reactive({
      title: "" as string,
      description: "" as string,
    });

    const addItemFun = () => {
      let newItem: Item = {
        id: lastNumber,
        imageUrl: `static/images/${lastNumber % 3}.png`,
        title: data.title,
        description: data.description,
        quantity: 0,
      } as Item;
      data.title = "";
      data.description = "";
      lastNumber++;
      emit("addItem", newItem as Item);
    };
    return { data, addItemFun };
  },
});
</script>

<style scoped>
.add-item-container {
  display: flex;
  flex-direction: column;
}
.add-item-container > *:not(:last-child) {
  margin-bottom: 10px;
}
.add-item-form-header {
  font-size: 1.3rem;
  /* font-variant: small-caps; */
  text-transform: uppercase;
}
.add-item-btn {
  border-radius: 8px;
  outline: unset;
  border: unset;
  padding: 10px;
  color: black;
  font-size: 1rem;
  cursor: pointer;
}
.add-item-btn:hover {
  box-shadow: 0px 0px 5px 1px #ccc;
}
</style>
