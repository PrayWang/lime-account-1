<template>
  <Layout>
    <Tabs class-prefix="type" :data-source="recordTypeList" :value.sync="type"/>
    <Chart :options="x"/>
    <ol v-if="groupedList.length>0">
      <li v-for="(group, index) in groupedList" :key="index">
        <h3 class="title">{{beautify(group.title)}} <span>￥{{group.total}}</span></h3>
        <ol>
          <li v-for="item in group.items" :key="item.id"
              class="record">
            <span>{{tagString(item.tags)}}</span>
            <span class="notes">{{item.notes}}</span>
            <span>￥{{item.amount}} </span>
          </li>
        </ol>
      </li>
    </ol>
    <div v-else class="noResult">
      <Icon name="blank2" /> <span>目前没有相关记录</span>
    </div>
  </Layout>
</template>
<script lang="ts">
import Tabs from '@/components/Tabs.vue';
import Vue from 'vue';
import {Component} from 'vue-property-decorator';
import recordTypeList from '@/constants/recordTypeList';
import dayjs from 'dayjs';
import clone from '@/lib/clone';
import Chart from '@/components/chart.vue';
import 'echarts/lib/chart/line';

@Component({
  components: {Tabs,Chart}
})
export default class Statistics extends Vue {
  tagString(tags:Tag[]){
    return  tags.length === 0 ? '无': tags.map(t=>t.name).join('，');
  }

  beautify(string:string){
    const day  = dayjs(string);
    const now  = dayjs();
    if(day.isSame(now,'day')){
     return '今天'
   }else if(day.isSame(now.subtract(1,'day'),'day')){
     return '昨天'
   }else if(day.isSame(now.subtract(2,'day'),'day')){
      return '前天'
    }else if(day.isSame(now,'year')){
      return day.format('M月D日')
    }else{
      return day.format('YYYY年M月D日')
    }
  }

  get x(){
    return{
      xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
      },
      yAxis: {
        type: 'value'
      },
      series: [
        {
          data: [120, 200, 150, 80, 70, 110, 130],
          type: 'line'
        }
      ],
      tooltip:{show:true}
    }
  }

  get recordList(){
    return (this.$store.state as RootState).recordList;
  }

  get groupedList() {
    const {recordList} = this;
    const newList = clone(recordList)
        .filter(r => r.type === this.type)
        .sort((a, b) => dayjs(b.createdAt).valueOf() - dayjs(a.createdAt).valueOf());
    if (newList.length === 0) {return [] as Result;}
    type Result = { title: string, total?: number, items: RecordItem[] }[]
    const result: Result = [{title: dayjs(newList[0].createdAt).format('YYYY-MM-DD'), items: [newList[0]]}];
    for (let i = 1; i < newList.length; i++) {
      const current = newList[i];
      const last = result[result.length - 1];
      if (dayjs(last.title).isSame(dayjs(current.createdAt), 'day')) {
        last.items.push(current);
      } else {
        result.push({title: dayjs(current.createdAt).format('YYYY-MM-DD'), items: [current]});
      }
    }
    result.map(group=>{
      group.total = group.items.reduce((sum,item)=>sum + item.amount,0)
    })

    return result;
  }

  beforeCreate(){
    this.$store.commit('fetchRecords')
  }

  type = '-';
  recordTypeList = recordTypeList;
};
</script>

<style scoped lang="scss">
.noResult{
  color: #999999;
  padding: 16px;
  text-align: center;
}
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