<template>
  <div id="app">
    <form @submit.prevent>
      <div class="formControl" :class="{error: $v.credentials.password.$error}">
        <input
          type="text"
          v-model="credentials.password"
          @blur="$v.credentials.password.$touch()"
          placeholder="password"
        >
      </div>
      <div class="formControl" :class="{error: $v.credentials.confirmPassword.$error}">
        <input
          type="text"
          v-model="credentials.confirmPassword"
          @blur="$v.credentials.confirmPassword.$touch()"
          placeholder="confirm password"
        >
      </div>
    </form>
  </div>
</template>

<script>
import { required, sameAs, minLength } from "vuelidate/lib/validators";
export default {
  name: "App",
  data() {
    return {
      credentials: {
        password: undefined,
        confirmPassword: undefined
      }
    };
  },
  validations: {
    credentials: {
      password: {
        required,
        minLength: minLength(5)
      },
      confirmPassword: {
        sameAs: sameAs(vm => {
          return vm.password || "";
        })
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
<style scoped>
div {
  padding: 10px;
}
.formControl.error input {
  border-color: red;
}
</style>
