<template>
  <div class="tabsWrapper">
    <Layout>
      <Tabs class-prefix="type" :data-source="recordTypeList" :value.sync="type"/>
      <Tabs class-prefix="interval" :data-source="intervalList" :value.sync="interval"/>
      <div>
        type:{{ type }}
        <br/>
        interval:{{ interval }}
      </div>
    </Layout>
  </div>
</template>

<style scoped lang="scss">
.tabsWrapper ::v-deep {
  .type-tabs-item {
    background: #5AD28C;

    &.selected {
      background: #25C877;
    }

    &.selected::after {
      background: #FEF3BB;
    }
  }

  .interval-tabs-item {
    height: 48px;
    background: white;
    color: #25C877;
    font-size: 20px;
    border: 1px solid #25C877;

    &.selected {
      background: #25C877;
      color: azure;
    }

    &.selected::after {
      display: none;
    }
  }
}

</style>

<script lang="ts">
import Tabs from '@/components/Tabs.vue';
import intervalList from '@/constants/intervalList';
import Vue from 'vue';
import {Component} from 'vue-property-decorator';
import recordTypeList from '@/constants/recordTypeList';

@Component({
  components: {Tabs}
})
export default class Statistics extends Vue {
  type = '-';
  interval = 'day';
  intervalList = intervalList;
  recordTypeList = recordTypeList;
};
</script>
