<template>
  <div>
    <div class="wrapper">
      <div>
        <img src="../assets/prat.png" v-bind:class="{ border_colored: isFocused}" />
      </div>
      <div>
        <p class="hugh_is" v-bind:class="{ blue: isFocused}">hugh is</p>
        <input
          ref="input"
          @input="handleChange"
          @focus="activeClass"
          @blur="unactiveClass"
          type="text"
          placeholder
          v-model="value"
          :style="{'width':`${this.width}px`}"
          v-bind:class="{ active: isFocused}"
        />
      </div>
      <div>
        <p class="hours_old">hours old</p>
      </div>
    </div>
    <div class="absolute">
      <span ref="span">{{this.value}}</span>
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      value: "",
      width: "",
      lastValue: "",
      isFocused: false
    };
  },
  methods: {
    setCursorPosition(el, pos) {
      el.focus();
      el.setSelectionRange(pos, pos);
    },
    activeClass() {
      this.isFocused = true;
      this.$emit("focused", this.isFocused);
    },
    unactiveClass() {
      this.isFocused = false;
      this.$emit("focused", this.isFocused);
    },
    handleChange() {
      this.$emit(
        "applied",
        this.value
          .replace(/[^\d]/g, "")
          .replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1 ")
      );

      /* eslint-disable */
      this.width = this.$refs.span.offsetWidth + 10;

      if (this.$refs.input.selectionStart < this.value.length) {
        const startPos = this.$refs.input.selectionStart;
        this.value = this.value
          .replace(/[^\d]/g, "")
          .replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1 ");

        this.$nextTick(() =>
          this.setCursorPosition(this.$refs.input, startPos)
        );
        this.lastValue = this.value;
        this.$emit("input-changed", this.value);
        return;
      }
      this.lastValue = this.value;
      this.value = this.value
        .replace(/[^\d]/g, "")
        .replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1 ");
      this.$emit("input-changed", this.value);
    }
  }
};
</script>
<style>
input {
  min-width: 50px !important;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  color: lightgray;
  margin-right: 8px;
}
.hugh_is {
  text-align: left;
  margin: 0;
  text-transform: uppercase;
  height: 17px;
  font-family: Roboto;
  font-size: 13px;
  font-weight: bold;
  font-stretch: condensed;
  font-style: normal;
  line-height: 1.31;
  letter-spacing: 0.8px;
}
.blue {
  color: blue;
}
.hours_old {
  padding-top: 12px;
  font-family: Roboto;
  font-size: 14px;
  font-weight: normal;
  font-stretch: normal;
  font-style: normal;
  line-height: 1.21;
  letter-spacing: normal;
}
span {
  visibility: hidden;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  width: 50px;
  min-width: 50px !important;
  color: lightgray;
  font-weight: bold;
  min-width: 50px;
  font-size: 11px;
}
.absolute {
  position: absolute;
}
.active {
  color: black;
  border-bottom: 1px solid blue;
}
.wrapper {
  display: flex;
  align-items: center;
}
</style>
