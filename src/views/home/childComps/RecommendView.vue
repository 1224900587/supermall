<template>
  <div class="recommendview">
    <div class="recommendview-item"
         v-for="item in recommends"
         :key="item.sort">
      <a :href="item.link">
        <img :src="item.image"
             alt="">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    recommends: {
      type: Array,
      default() {
        return []
      },
    },
  },
}
</script>

<style acoped>
.recommendview {
  display: flex;
  width: 100%;
  padding-bottom: 30px;
  border-bottom: 8px solid #eee;
}

.recommendview-item {
  flex: 1;
  text-align: center;
}

.recommendview-item img {
  width: 70px;
  height: 70px;
  margin-top: 10px;
}
</style>