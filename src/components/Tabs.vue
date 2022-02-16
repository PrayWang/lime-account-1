<template>
  <ul class="tabs" :class="{[classPrefix+'-tabs']:classPrefix}">
    <li v-for="item in dataSource" :key="item.value"
        class="tabs-item"
        :class="liClass(item)"
    @click="select(item)">{{item.text}}</li>
  </ul>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';

type DataSourceItem = {text:string,value:string}

@Component
export default class Tabs extends Vue {
  @Prop({required:true,type:Array})
  dataSource!:DataSourceItem[]
  @Prop(String) readonly value!:string;
  @Prop(String) classPrefix?:string;

  liClass(item:DataSourceItem){
    return{
      selected:item.value===this.value,
      [this.classPrefix + '-tabs-item']:this.classPrefix
    }
  };

  select(item:DataSourceItem){
      this.$emit('update:value',item.value)
  }
}
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";

.tabs {
  display: flex;
  text-align: center;
  font-size: 24px;
  color: azure;
  background: #5AD28C;

  &-item {
    width: 50%;
    height: 7vh;
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