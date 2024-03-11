<template>
  <form @submit.prevent="Login">
    <div class="form_group">
      <input
        v-model="username"
        class="input_error form_input"
        placeholder="Username"
        type="text"
        data-test="username"
        id="username"
        name="username"
        autocorrect="off"
        autocapitalize="none"
        :class="{ error: errorMessage }"
      />
      <img
        src="../../assets/img/close.png"
        class="error_icon"
        :hidden="!iserror"
      />
    </div>

    <div class="form_group">
      <input
        v-model="password"
        class="input_error form_input"
        placeholder="Password"
        type="password"
        data-test="password"
        id="password"
        name="password"
        autocorrect="off"
        autocapitalize="none"
        :class="{ error: errorMessage }"
      />
      <img
        src="../../assets/img/close.png"
        class="error_icon"
        :hidden="!iserror"
      />
    </div>

    <div class="error_message_container" :class="{ error: errorMessage }">
      <h3 data-test="error" :hidden="!iserror">
        <button type="button" class="error_button" @click="resetError">
          <img
            src="../../assets/img/close.png"
            class="cross_icon"
            alt="Close Menu"
          />
        </button>
        {{ errorMessage }}
      </h3>
    </div>

    <input
      type="submit"
      class="submit_button btn_action"
      id="login_button"
      name="login_button"
      value="Login"
    />
  </form>
</template>

<script setup>
import { ref } from "vue";

var username = ref("");
var password = ref("");
var iserror = ref(false);
var errorMessage = ref("");

var usernamelist = [
  "standard_user",
  "locked_out_user",
  "problem_user",
  "performance_glitch_user",
  "error_user",
  "visual_user",
];

var passwordlist = ["secret_sauce"];

const Login = () => {
  if (
    usernamelist.includes(username.value) &&
    passwordlist.includes(password.value)
  ) {
    window.location.href = "/inventory";
  } else {
    iserror.value = true;

    if (iserror.value) {
      if (username.value === "") {
        errorMessage.value = "Epic sadface: Username is required";
      } else if (password.value === "") {
        errorMessage.value = "Epic sadface: Password is required";
      } else {
        errorMessage.value =
          "Epic sadface: Username and password do not match any user in this service";
      }
    } else {
      iserror.value = !iserror.value;
    }
  }
};

const resetError = () => {
  iserror.value = false;
  errorMessage.value = "";
};
</script>
