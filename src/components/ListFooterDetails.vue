<template>
  <div class="card footer-details">
    <div class="showing-counter">
      Showing {{ showingItemCount }} of {{ totalItemCount }} items
    </div>
    <div class="quantity-showing-counter">
      Total counter quantities {{ totalShowenQuantityCount }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "ListFooterDetails",
  props: {
    showingItemCount: { type: Number },
    totalItemCount: { type: Number },
    totalShowenQuantityCount: { type: Number },
  },
});
</script>

<style scoped>
.footer-details {
  display: flex;
  justify-content: space-between;
}
</style>
