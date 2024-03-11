<template>
  <div class="secondary_header">
    <span class="page_title">{{ page_title }}</span>
    <div class="filter">
      <span class="sort">
        <span class="active_option">{{ selectedSortText }}</span>
        <select
          class="product_sort"
          v-model="selectedSort"
          @change="updateSort"
        >
          <option value="az">Name (A to Z)</option>
          <option value="za">Name (Z to A)</option>
          <option value="lowhigh">Price (low to high)</option>
          <option value="highlow">Price (high to low)</option>
        </select>
      </span>
    </div>
  </div>

  <div class="inventory_container">
    <div class="inventory_list">
      <div class="inventory_item" v-for="item in filteredItems" :key="item.id">
        <div class="inventory_item_img">
          <a href="#" :id="`item_${item.id}_img_link`">
            <img :src="item.img" class="inventory_item_image" />
          </a>
        </div>
        <div class="inventory_item_description">
          <div class="inventory_item_label">
            <a href="#" :id="`item_${item.id}_title_link`">
              <div class="inventory_item_name">{{ item.name }}</div>
            </a>
            <div class="inventory_item_desc">{{ item.description }}</div>
          </div>
          <div class="pricebar">
            <div class="inventory_item_price">${{ item.price }}</div>
            <button class="btn btn_primary btn_small">Add to cart</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import itemlist from "../components/itemlist.js";
import "../styles/InventoryListItem.css";
import "../styles/Button.css";
import "../styles/Filter.css";

import { ref, computed } from "vue";

const props = defineProps({
  page_title: String,
});

const page_title = props.page_title;

var selectedSort = ref("az"); // Default sort value

// Function to update the selected sort value
const updateSort = (event) => {
  selectedSort.value = event.target.value;
};

// Computed property to dynamically generate the sort text based on the selected option
const selectedSortText = computed(() => {
  switch (selectedSort.value) {
    case "az":
      return "Name (A to Z)";
    case "za":
      return "Name (Z to A)";
    case "lowhigh":
      return "Price (low to high)";
    case "highlow":
      return "Price (high to low)";
    default:
      return "";
  }
});

// Computed property to filter the items based on the selected sort value
const filteredItems = computed(() => {
  // Get the current value of selectedSort
  var sortValue = selectedSort.value;

  // Logic to filter the items based on the selected sort value
  if (sortValue === "az") {
    return itemlist.items.sort((a, b) => a.name.localeCompare(b.name));
  } else if (sortValue === "za") {
    return itemlist.items.sort((a, b) => b.name.localeCompare(a.name));
  } else if (sortValue === "lowhigh") {
    return itemlist.items.slice().sort((a, b) => {
      if (a.price === b.price) {
        // If prices are the same, sort by name alphabetically
        return a.name.localeCompare(b.name);
      } else {
        // Otherwise, sort by price from low to high
        return a.price - b.price;
      }
    });
  } else if (sortValue === "highlow") {
    return itemlist.items.slice().sort((a, b) => {
      if (a.price === b.price) {
        // If prices are the same, sort by name alphabetically in reverse order (Z to A)
        return a.name.localeCompare(b.name);
      } else {
        // Otherwise, sort by price from high to low
        return b.price - a.price;
      }
    });
  } else {
    return itemlist.items; // Default sorting
  }
});
</script>
