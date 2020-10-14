<template>
  <div class="nav-bar">
    <div class="left">
      <slot></slot>
    </div>
    <div class="center">
      <slot></slot>
    </div>
    <div class="right">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
.nav-bar {
  display: flex;
  height: 44px;
  line-height: 44px;
  box-shadow: 0px 1px 1px rgba(100, 100, 100, 0.1);
}

.left,
.right {
  width: 60px;
}

.center {
  flex: 1;
}
</style>