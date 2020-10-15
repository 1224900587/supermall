<template>
  <div class="tab-control">
    <div class="tab-control-item"
         v-for="(item,index) in titles"
         :key="index"
         :class="{controlActive:currControlindex==index}"
         @click="clickControl(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    titles: {
      type: Array,
      default() {
        return []
      },
    },
  },
  data() {
    return {
      currControlindex: 0,
    }
  },
  methods: {
    clickControl(index) {
      this.currControlindex = index
      this.$emit('cilckcon',index)
    },
  },
}
</script>

<style scoped>
.tab-control {
  display: flex;
  background-color: #fff;
  text-align: center;
  height: 40px;
  line-height: 40px;
  font-size: 15px;
  position: sticky;
  top: 0;
}

.tab-control-item {
  flex: 1;
}

.controlActive {
  color: var(--color-high-text);
}

.controlActive span {
  padding: 2px;
  border-bottom: 2px solid var(--color-high-text);
}
</style>