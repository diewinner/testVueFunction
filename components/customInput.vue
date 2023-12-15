<template>
  <input type="text" @input="$emit('input',$event.target.value)" class="input"/>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss" scoped>
input {
  border: 1px solid black;
  outline: none;
  padding: 5px 10px;

  &:focus {
    border: 1px solid #2A3C93FF;
    box-shadow: 1px 1px 2px 0 #2A3C93FF;
  }
}
</style>
