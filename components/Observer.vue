<template>
  <div class="observer"/>
</template>

<script>
export default {
  name: 'Observer',
  props: {
    options: {
      type: String,
      default: ''
    }
  },
  data: () => ({
    observer: null
  }),
  mounted() {
    const options = this.options || {};
    this.observer = new IntersectionObserver(([entry]) => {
      if (entry && entry.isIntersecting) {
        this.$emit('intersect');
      }
    }, options);

    this.observer.observe(this.$el);
  },
  destroyed() {
    this.observer.disconnect();
  }
};
</script>
