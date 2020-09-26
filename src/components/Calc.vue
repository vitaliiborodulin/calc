<template lang="pug">
  v-container
    v-row(justify="center")
     v-col(cols="12" md="4")
      v-row
        v-col(cols="12")
          .input-display.text-right {{valueDisplayed}}
      v-row
        v-col
          v-btn.secondary(@click="reset()" block) Сброс
      v-row
        v-col(cols="3" v-for="operation in operations")
          v-btn.primary(@click="handleDigit(operation.text)"
            v-if="operation.type === 'number'" block) {{operation.text}}
          v-btn.primary(@click="handleOp(operation.text)"
            v-else block) {{operation.text}}
</template>

<script>
export default {
  name: 'Calc',
  data: () => ({
    currentValue: 0,
    savedValue: 0,
    currentOp: false,
    operations: [
      { text: '7', type: 'number' },
      { text: '8', type: 'number' },
      { text: '9', type: 'number' },
      { text: '*', type: 'op' },
      { text: '4', type: 'number' },
      { text: '5', type: 'number' },
      { text: '6', type: 'number' },
      { text: '-', type: 'op' },
      { text: '1', type: 'number' },
      { text: '2', type: 'number' },
      { text: '3', type: 'number' },
      { text: '+', type: 'op' },
      { text: '/', type: 'op' },
      { text: '0', type: 'number' },
      { text: '.', type: 'number' },
      { text: '=', type: 'op' },
    ],
  }),
  methods: {
    reset() {
      this.currentValue = 0;
      this.savedValue = 0;
      this.currentOp = false;
    },
    handleDigit(digit) {
      this.currentValue = (this.currentValue) ? this.currentValue + digit : digit;
    },
    handleOp(op) {
      if (this.currentOp) {
        this.process();
      } else {
        this.savedValue = parseFloat(this.currentValue);
      }
      this.currentValue = 0;
      this.currentOp = op;
    },
    process() {
      const currentValueNumber = parseFloat(this.currentValue);

      switch (this.currentOp) {
        case '*':
          this.savedValue *= currentValueNumber;
          break;
        case '/':
          this.savedValue /= currentValueNumber;
          break;
        case '+':
          this.savedValue += currentValueNumber;
          break;
        case '-':
          this.savedValue -= currentValueNumber;
          break;
        default:
          this.savedValue = currentValueNumber;
          break;
      }
    },
  },
  computed: {
    valueDisplayed() {
      return (this.savedValue && !this.currentValue) ? this.savedValue : this.currentValue;
    },
  },
};
</script>

<style lang="sass">
.input-display
  background: black
  color: white
  font-size: xx-large
  padding: 12px
</style>
