<template>
  <div>
    <div>
      <div class="hamburger">
        <button class="hamburger_button" @click="ToggleMenu"></button>
        <img src="../../assets/svg/hamburger_menu.svg" class="hamburger_icon" />
      </div>
    </div>

    <div class="menu_container" :class="{ visible: hidden }">
      <div class="menu_list">
        <nav class="item_list">
          <a id="inventory" class="item menu_item" href="#">All Items</a>
          <a
            id="about"
            class="item menu_item"
            href="https://saucelabs.com/"
            target="_blank"
            >About</a
          >
          <a id="logout" class="item menu_item" href="/">Logout</a>
          <a id="reset" class="item menu_item" href="#">Reset App State</a>
        </nav>
      </div>

      <div>
        <div class="cross_button">
          <button class="close_button" @click="ToggleMenu"></button>
          <img
            src="../../assets/svg/close.svg"
            class="cross_icon"
            alt="Close Menu"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
var hidden = ref(false);

const ToggleMenu = () => {
  hidden.value = !hidden.value;
};
</script>
