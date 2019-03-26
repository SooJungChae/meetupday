<template>
	<div class="day-wrap">
    <div
      :class="{active: dragging}"
      @mousedown="startDrag"
      @mousemove="move"
      @dragenter="startDrag"
      @mouseup="stopDrag">{{dragging}}</div>
  </div>
</template>

<script>
export default {
	name: "Day",
  props: ['dragging'],
  methods: {
    startDrag () {
      this.$emit('set', true);
    },
    move (e) {
      if (this.dragging) {
        console.log(e);
        // e.target.classList.add('active');
        // console.log('move');
      }
    },
    stopDrag () {
      this.$emit('set', false);
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
}
</style>
