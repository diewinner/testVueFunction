<template>
  <button class="v_button" @click="click">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: 'vButton',
  props: {
    text: {
      type: String,
      default: ''
    }
  },
  methods: {
    click() {
      this.$emit('click')
    }
  },

}
</script>

<style lang="scss" scoped>
.v_button {
  width: 100%;
  height: 100%;
  padding: 0.4em 0.5em;
  background: transparent;
  border: 1px solid black;
  border-radius: 5px;
  transition: all 0.3s ease-in-out;
  cursor: pointer;

  &:hover {
    background: black;
    color: white;
    transform: scale(.95);
  }
}
</style>
