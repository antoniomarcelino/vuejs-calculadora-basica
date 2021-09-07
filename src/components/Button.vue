<template>
  <div @click="append()" class="button">{{value}}</div>
</template>

<script>
export default {
    props: {
        value: {
            type: String,
            required: true
        }
    },
    methods: {
        append() {
            this.$emit('append', this.value)
        }
    }
}
</script>

<style scoped>
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