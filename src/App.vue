<template>
  <AddingForm @addItem="addItemToList"></AddingForm>
  <SearchForm
    placeholder="Search by title or description ..."
    v-model="data.searchingText"
  ></SearchForm>
  <ListItem
    v-for="item in filteredList"
    :item="item"
    :key="item.id"
    @changeQuantityBy="changeQuantityBy"
  ></ListItem>
  <div class="card text-center" v-if="totalItemCount <= 0">
    The item list is empty please add new one
  </div>
  <div class="card text-center" v-else-if="totalShowingItemCount <= 0">
    Can't find any item with the search text
  </div>
  <ListFooterDetails
    :total-item-count="totalItemCount"
    :showing-item-count="totalShowingItemCount"
    :total-showen-quantity-count="totalQuantitiesShowenCount"
  ></ListFooterDetails>
</template>

<script lang="ts">
import { computed, defineComponent, reactive } from "vue";
import AddingForm from "@/components/AddingForm.vue";
import ListFooterDetails from "@/components/ListFooterDetails.vue";
import { Item } from "@/Interfaces/Item";
import ListItem from "@/components/ListItem.vue";
import SearchForm from "@/components/SearchForm.vue";

export default defineComponent({
  name: "App",
  components: {
    SearchForm,
    ListItem,
    ListFooterDetails,
    AddingForm,
  },
  setup() {
    //Data
    const data = reactive({
      itemList: [] as Item[],
      searchingText: "" as string,
    });
    //searching
    const filteredList = computed(() =>
      data.itemList.filter(
        (i) =>
          i.title.toLowerCase().includes(data.searchingText.toLowerCase()) ||
          i.description.toLowerCase().includes(data.searchingText.toLowerCase())
      )
    );
    //counters
    const totalItemCount = computed(() => data.itemList.length);
    const totalShowingItemCount = computed(() => {
      return filteredList.value.length;
    });
    const totalQuantitiesShowenCount = computed(() => {
      let total = 0;
      if (filteredList.value && filteredList.value.length) {
        total = filteredList.value
          .map((i) => i.quantity)
          .reduce((prevQuantity, nextQuantity) => {
            return prevQuantity + nextQuantity;
          });
      }
      return total;
    });

    //Adding item to the list
    const addItemToList = (item: Item) => {
      data.itemList.push(item as Item);
      // console.log(data.itemList);
    };

    //changing the quantity on specific item
    const changeQuantityBy = (itemId: number, amount: number) => {
      // the amount it could be positive value or negative value
      //get the object from the array
      const itemObj = data.itemList.find((i) => {
        return i.id === itemId;
      });
      if (itemObj) {
        itemObj.quantity += amount;
      }
    };
    return {
      data,
      addItemToList,
      filteredList,
      changeQuantityBy,
      totalItemCount,
      totalShowingItemCount,
      totalQuantitiesShowenCount,
    };
  },
});
</script>

<style src="./assets/css/general.css"></style>
