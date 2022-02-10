<template>
  <div class="x">
    <Layout>
      <Tabs class-prefix="type" :data-source="recordTypeList" :value.sync="type"/>
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
import intervalList from '@/constants/intervalList';
import Vue from 'vue';
import {Component} from 'vue-property-decorator';
import recordTypeList from '@/constants/recordTypeList';

@Component({
  components:{Types,Tabs}
})
export default class Statistics extends Vue{
  type='-';
  interval='day';
  intervalList = intervalList;
  recordTypeList = recordTypeList;
};
</script>
