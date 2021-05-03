<template>
  <div class="card list-item-container">
    <div class="item-image-container">
      <img class="item-image" :src="item.imageUrl" />
    </div>
    <div class="item-details">
      <div class="item-title">{{ item.title }}</div>
      <div class="item-description">{{ item.description }}</div>
    </div>
    <div class="item-quentity">
      <button class="item-decrement" @click="decrement">-</button>
      <span class="item-quentity-value">{{ item.quantity }}</span>
      <button class="item-increase" @click="increment">+</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
// import { Item } from "@/Interfaces/Item";

export default defineComponent({
  name: "ListItem",
  props: {
    item: {
      type: Object,
    },
  },
  setup(props, { emit }) {
    const increment = () => {
      emit("changeQuantityBy", props.item?.id, 1);
    };
    const decrement = () => {
      emit("changeQuantityBy", props.item?.id, -1);
    };
    return { increment, decrement };
  },
});
</script>

<style scoped>
.list-item-container {
  display: flex;
}
.item-image-container {
  padding-right: 10px;
  margin-right: 10px;
  border-right: 1px solid rgba(0, 0, 0, 0.05);
}
.item-image-container .item-image {
  width: 100%;
  max-width: 150px;
}
.item-details {
  flex: 1;
}
.item-details .item-title {
  font-size: 1.375rem;
  margin-bottom: 10px;
}

.item-details .item-description {
  font-size: 1.125rem;
}
.item-quentity {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}
.item-quentity .item-decrement,
.item-quentity .item-increase {
  cursor: pointer;
  padding: unset;
  font-size: 1.375rem;
  border: 0;
  background-color: rgba(0, 0, 0, 0.1);
  color: #616161;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.item-quentity .item-decrement:hover,
.item-quentity .item-increase:hover {
  box-shadow: 0px 0px 8px 2px rgba(213, 213, 213, 0.56);
  color: black;
}
.item-quentity .item-quentity-value {
  margin: 0px 10px;
}
</style>
