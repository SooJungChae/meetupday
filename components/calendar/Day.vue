<template>
	<div class="day-wrap">
    <div
      :class="{select: toggleSelect}"
      @mousedown="onmousedown"
      @mouseover="onmouseover">{{dragging}}</div>
  </div>
</template>

<script>
export default {
	name: "Day",
  props: ['dragging'],
  data () {
	  return {
      toggleSelect: false
    }
  },
  methods: {
    onmousedown (e) {
      this.toggleSelect = !this.toggleSelect;
    },
    onmouseover (e) {
      if (this.dragging) {
        this.toggleSelect = !this.toggleSelect;
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
