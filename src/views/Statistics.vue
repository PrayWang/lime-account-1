<template>
  <div class="x">
    <Layout>
      <Tabs class-prefix="type" :data-source="typeList" :value.sync="type"/>
      <Tabs class-prefix="interval" :data-source="intervalList" :value.sync="interval"/>
      <div>
        type:{{type}}
        <br/>
        interval:{{interval}}
      </div>
    </Layout>
  </div>
</template>

<style scoped lang="scss">
 .x ::v-deep .type-tabs-item{
    &.selected::after {
     content: '';
     position: absolute;
     bottom: 0;
     left: 0;
     width: 100%;
     height: 4px;
     background: #FEF3BB;
   }
 }
</style>

<script lang="ts">
import Types from '@/components/Money/Types.vue';
import Tabs from '@/components/Tabs.vue';
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

@Component({
  components:{Types,Tabs}
})
export default class Statistics extends Vue{
  type='-';
  interval='day';
  intervalList = [
    {text:'按天',value:'day'},
    {text:'按周',value:'week'},
    {text:'按月',value:'mouth'}
  ];
  typeList = [
    {text:'支出',value:'-'},
    {text:'收入',value:'+'}
  ]
};
</script>
