<template>
  <button class="button"
    @click="$emit('onCalcBtnClick', label)"
    :class="{double, triple, operation}">
    {{ label }}
  </button>
</template>

<script>
export default {
  props: {
    label: {},
    operation: {type: Boolean},
    double: {type: Boolean},
    triple: {type: Boolean}
  }
}
</script>

<style>
  :root {
    --bg-button:  #f0f0f0;
    --border-button: solid 1px #888;
  }

  .button {
    font-size: 1.4em;
    background-color: var(--bg-button);
    border: none;
    border-right: var(--border-button);
    border-bottom: var(--border-button);
    outline: none;
  }

  .button:active {
    background-color: #888888;
  }

  .button.double {
    grid-column: span 2;
  }

  .button.triple {
    grid-column: span 3;
  }

  .button.operation {
    background-color: orange;
    color: #fff;
  }

  .button.operation:active {
    background-color: rgb(191, 124, 1);
  }
</style>