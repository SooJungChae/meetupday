<template>
	<div class="day-wrap">
    <div
      :class="{select: toggleSelect}"
      @mousedown="onmousedown"
      @mouseover="onmouseover"
    >{{value}}</div>
  </div>
</template>

<script>
export default {
	name: "Day",
  props: ['dragging', 'value'],
  data () {
	  return {
      toggleSelect: false
    }
  },
  methods: {
    onmousedown (e) {
      this.toggleSelect = !this.toggleSelect;
      this.$emit('set', { index: this.value, value: this.toggleSelect});
    },
    onmouseover (e) {
      if (this.dragging) {
        this.toggleSelect = !this.toggleSelect;
        this.$emit('set', { index: this.value, value: this.toggleSelect});
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.day-wrap {
  width: 100%;
  height: 100%;

  button {
    width: 100%;
    height: 100%;

  }

  .select {
    background-color: red;
  }
}
</style>
