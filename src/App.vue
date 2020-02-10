<template>
  <div id="app">
    <div class="separate">
      <Input @applied="handleChange" @focused="handleFocus" />
    </div>
    <div class="separate">
      <Input @applied="handleChange" @focused="handleFocus" />
    </div>
  </div>
</template>

<script>
import Input from "./components/Input.vue";

export default {
  name: "app",
  components: {
    Input
  },
  data: () => {
    return {
      focus: false
    };
  },
  methods: {
    handleChange(inputValue) {
      /* eslint-disable */
      console.log(inputValue);
    },
    handleFocus(isFocused) {
      /* eslint-disable */
      this.focus = isFocused;
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Roboto+Condensed");
p {
  font-family: "Roboto Condensed", sans-serif;
}
.input-wrapper {
  display: flex;
  align-items: center;
}
img {
  width: 55px;
  border-radius: 50%;
  margin-right: 16px;
}
.border_colored {
  border: solid 1px blue;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input {
  width: 50px;
  outline: none;
  appearance: none;
  border: none;
  font-weight: bold;
  padding-bottom: 8px;
  border-bottom: 1px solid grey;
}
.separate {
  margin-top: 32px;
}
</style>
