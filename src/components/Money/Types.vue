<template>
  <div>
    <ul class="types">
      <li class="pay" :class="type === '-' && 'selected'" @click="selectType('-')">支出</li>
      <li class="income" :class="type === '+' && 'selected'" @click="selectType('+')">收入</li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

@Component
export default class Types extends Vue {
  type = '-';//'-'表示支出,'+'表示收入
  selectType(type: string) {
    if (type !== '-' && type !== '+') {
      throw new Error('type is unknown');
    }
    this.type = type;
  }
}
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";

.types {
  display: flex;
  text-align: center;
  font-size: 24px;
  color: azure;
  background: #5AD28C;

  > li {
    width: 50%;
    height: 64px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    &.selected {
      background: #25C877;
    }

    &.selected::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 4px;
      background: #F2A291;
    }
  }
}
</style>