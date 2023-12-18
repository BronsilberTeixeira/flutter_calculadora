<template>
  <div class="calculator">
    <DisplayCalculadora :value="displayValue" />
    <BotaoCalculadora label="AC" triple @onCalcBtnClick="clearMemoria" />
    <BotaoCalculadora label="/" operation @onCalcBtnClick="setOperation" />
    <BotaoCalculadora label="7" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="8" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="9" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="*" operation @onCalcBtnClick="setOperation" />
    <BotaoCalculadora label="4" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="5" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="6" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="-" operation @onCalcBtnClick="setOperation" />
    <BotaoCalculadora label="1" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="2" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="3" @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="+" operation @onCalcBtnClick="setOperation" />
    <BotaoCalculadora label="0" @onCalcBtnClick="addDigit" double />
    <BotaoCalculadora label="." @onCalcBtnClick="addDigit" />
    <BotaoCalculadora label="=" operation @onCalcBtnClick="setOperation" />
  </div>
</template>

<script>
import BotaoCalculadora from "./BotaoCalculadora";
import DisplayCalculadora from "./DisplayCalculadora";

export default {
  data: function () {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0
    };
  },
  components: { BotaoCalculadora, DisplayCalculadora },
  methods: {
    clearMemoria() {
      Object.assign(this.$data, this.$options.data());
    },
    setOperation(operation) {
      if (this.current === 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;

        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.values[1]}`
          );
        } catch (e) {
          this.$emit("onError", e);
        }

        this.values[1] = 0

        this.displayValue = this.values[0]
        console.log(this.values[0]);
        this.operation = equals ? null : operation
        this.current = equals ? 0 : 1
        this.clearDisplay = !equals
      }
    },
    addDigit(n) {
      if (n === "." && this.displayValue.includes(".")) {
        return;
      }
      const clearDisplay = this.displayValue === "0" || this.clearDisplay;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const displayValue = currentValue + n;

      this.displayValue = displayValue;
      this.clearDisplay = false;
      this.values[this.current] = this.displayValue
    },
  },
};
</script>

<style>
.calculator {
  height: 320px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden;

  display: grid;
  grid-template: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px;
}
</style>