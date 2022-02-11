<template>
  <div class="tabsWrapper">
    <Layout>
      <Tabs class-prefix="type" :data-source="recordTypeList" :value.sync="type"/>
      <Tabs class-prefix="interval" :data-source="intervalList" :value.sync="interval"/>
        <ol>
          <li v-for="(group,index) in result" :key="index">
            <h3 class="title">title</h3>
            <ol>
              <li v-for="item in group" :key="item.id" class="record">
                <span>{{tagString(item.tags)}}</span>
                <span  class="notes">{{item.notes}}</span>
                <span>￥{{item.amount}}</span>
              </li>
            </ol>
          </li>
        </ol>
    </Layout>
  </div>
</template>

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
  tagString(tags:Tag[]){
    return  tags.length === 0 ? '无': tags.join(',');
  }
  get recordList(){
    return (this.$store.state as RootState).recordList;
  }

  get result(){
    const {recordList} = this;
    // type HashTableValue = {title:string,items: RecordList[]}
    // const hashTable : {[key:string] : HashTableValue} = {};
    const hashTable:{[key:string]:RecordItem[]}={};
    for(let i=0;i<recordList.length;i++){
     const [date,time] = recordList[i].createdAt!.split('T');
     console.log(date);
     hashTable[date] = hashTable[date] || []
      // hashTable[date].items.push({recordList[i]})
      hashTable[date].push(recordList[i]);
    }
    console.log(hashTable);
    return hashTable;
  }

  beforeCreate(){
    this.$store.commit('fetchRecords')
  }

  type = '-';
  interval = 'day';
  intervalList = intervalList;
  recordTypeList = recordTypeList;
};
</script>

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
%item{
  padding: 8px 16px;
  line-height: 24px;
  display: flex;
  justify-content: space-between;
  align-content: center;
}
.title{
  @extend %item;
}

.record{
  background: white;
  @extend %item;
}

.notes{
  margin-right: auto;
  margin-left: 16px;
  color: #999999;
}
</style>