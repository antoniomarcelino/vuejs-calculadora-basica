<template>
  <div @click="assignOperation()" class="operator-button">{{operator}}</div>
</template>

<script>
export default {
    props: {
        operator: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            operation: null,
        }
    },
    methods: {
        assignOperation() {
            switch(this.operator) {
                case "÷": 
                    this.operation = (a, b) => a / b
                    break
                case "x":
                    this.operation = (a, b) => a * b
                    break
                case "-":
                    this.operation = (a, b) => a - b
                    break
                case "+":
                    this.operation = (a, b) => a + b
                    break
                case "=":
                    this.$emit('equal')
                    break
                case ".":
                    this.$emit('dot')
                    break
            }
            if(this.operator !== '=' && this.operator !== '.')
                this.$emit('assign', this.operation)
        }
    }
}
</script>

<style scoped>
.operator-button {
  border: 1px solid #646468;
  background-color: #ef9741;
  color: white;
  padding: 20px;
}

.operator-button:hover {
    color: #2c3e50;
    cursor: pointer;
}
</style>