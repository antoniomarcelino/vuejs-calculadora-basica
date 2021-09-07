<template>
<div>
  <h1 style="padding: 1rem 0; font-weight: bold;">Calculadora Básica</h1>
  <div class="calculator">
      
    <div class="display">{{ current || '0' }}</div>

    <div @click="clear" class="button">C</div>
    <div @click="sign" class="button">+/-</div>
    <div @click="percent" class="button">%</div>
    <OperatorButton :operator="'÷'" @assign="(operation) => assignOperation(operation)" />

    <Button :value="7" @append="(value) => append(value)"/>
    <Button :value="8" @append="(value) => append(value)"/>
    <Button :value="9" @append="(value) => append(value)"/>
    <OperatorButton :operator="'x'" @assign="(operation) => assignOperation(operation)" />

    <Button :value="4" @append="(value) => append(value)"/>
    <Button :value="5" @append="(value) => append(value)"/>
    <Button :value="6" @append="(value) => append(value)"/>
    <OperatorButton :operator="'-'" @assign="(operation) => assignOperation(operation)" />

    <Button :value="1" @append="(value) => append(value)"/>
    <Button :value="2" @append="(value) => append(value)"/>
    <Button :value="3" @append="(value) => append(value)"/>
    <OperatorButton :operator="'+'" @assign="(operation) => assignOperation(operation)" />

    <Button id="zero" :value="0" @append="(value) => append(value)"/>
    <OperatorButton :operator="'.'" @dot="dot()" />
    <OperatorButton :operator="'='" @equal="equal()" />
  </div>
  <h5 style="padding: 1rem 0;">Esta é uma calculadora básica criada com VUE JS.</h5>
</div>
  
</template>

<script>
import Button from './Button.vue'
import OperatorButton from './OperatorButton.vue'

export default {
  name: 'HelloWorld',
  data() {
    return {
      current: '',
      operation: null,
      previous: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = ''
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    assignOperation(operation) {
      this.operation = operation
      this.operatorClicked = true
      this.previous = this.current
    },
    equal() {
      this.current = `${this.operation (
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`
      this.previous = null
    }
  },
  components: {
    Button,
    OperatorButton,
  }
 
}
</script>

<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 38px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.display {
  grid-column: 1 / 5;
  color: white;
  background: #37548f;
  padding: 20px;
}

#zero {
  grid-column: 1/3;
}

.button {
  background-color: #d4d3d5;
  border: 1px solid #646468;
  padding: 20px;
}

.button:hover {
    color: #ef9741;
    cursor: pointer;
}
</style>
