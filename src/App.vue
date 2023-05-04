<!--
 * @Author: 王川王川 wc@oetsky.com
 * @Date: 2023-04-13 09:58:26
 * @LastEditors: 王川王川 wc@oetsky.com
 * @LastEditTime: 2023-04-13 11:10:15
 * @FilePath: \vue3-grid-layout\src\App.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <grid-layout v-model:layout="layout" :col-num="3" :row-height="250" :is-draggable="true" :is-resizable="true"
    :is-mirrored="false" :vertical-compact="true" :placeholderHeight="0.1" :margin="[10, 20]" :use-css-transforms="true">
    <grid-item v-for="item in layout" :key="item.i" drag-allow-from=".toolbox" v-bind="item" @move="movedEvent">
      <div class="card">
        <div class="card-header toolbox">
          drag
          <span class="remove" @click="removeItem(item.i)">x</span>
        </div>
        <div class="card-main">
          {{ item.i }}
          <br />
        </div>
      </div>
    </grid-item>
  </grid-layout>
</template>

<script setup lang="ts">
import { ref } from 'vue';
const movedEvent = () => {
  return false;
}
const removeItem = (val) => {
  const index = layout.value.map(item => item.i).indexOf(val);
  layout.value.splice(index, 1);
}
const layout = ref([
  { x: 0, y: 0, w: 2, h: 1, i: '1', static: false, minH: 5 },
  { x: 0, y: 1, w: 2, h: 1, i: '2', static: false, minH: 5 },
  { x: 2, y: 0, w: 1, h: 1, i: '3', static: false, minH: 5 },
  { x: 2, y: 1, w: 1, h: 1, i: '4', static: false, minH: 5 },
])
</script>
<style lang="scss">
.card {
  display: flex;
  flex-direction: column;
  height: 100%;
  position: relative;
  border: 1px solid #e9ebf0;
  border-radius: 4px;

  .card-header {
    display: flex;
    padding: 0 20px;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 40px;
    text-align: center;
    box-sizing: border-box;
  }

  .card-main {
    background: #f2f5f7;
    height: 100%;
    text-align: center;
    margin: 0 20px 20px 20px;
  }

  .remove {
    cursor: pointer;
  }
}
</style>