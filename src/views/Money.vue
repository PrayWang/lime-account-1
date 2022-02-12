<template>
  <div>
    <layout class-prefix="layout">
      <NumberPad @update:value="onUpdateAmount" @submit="saveRecord"/>
      <div class="notes-wrapper">
        <FormItem field-name="备注" placeholder="请输入备注"
        :value.sync="record.notes"/>
      </div>
      <Tags @update:value="record.tags = $event"  />
      <Tabs :data-source="recordTypeList"
      :value.sync="record.type"/>
    </layout>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import NumberPad from '@/components/Money/NumberPad.vue';
import Tags from '@/components/Money/Tags.vue';
import {Component} from 'vue-property-decorator';
import FormItem from '@/components/Money/formItem.vue';
import Tabs from '@/components/Tabs.vue';
import recordTypeList from '@/constants/recordTypeList';

@Component({
  components: {FormItem, Tags, NumberPad,Tabs},
  },
)
export default class Money extends Vue {
  get recordList(){
    return this.$store.state.recordList;
  }
  record: RecordItem = {
    tags: [], notes: '', type: '-', amount: 0,createRecordError:null
  };

  created(){
    this.$store.commit('fetchRecords')
  }

  onUpdateNotes(value: string) {
    this.record.notes = value;
  }

  onUpdateAmount(value: string) {
    this.record.amount = parseFloat(value);
  }

  saveRecord() {
    if(!this.record.tags||this.record.tags.length === 0){
      return window.alert('请至少选择一个标签');
    }
    this.$store.commit('createRecord',this.record);
    if(this.$store.state.createRecordError === null){
      window.alert('已保存');
      this.record.notes = '';
    }
  }
  recordTypeList = recordTypeList;
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}

.notes-wrapper {
  border: 3px solid #25C877;
  border-radius: 10px;
  background: rgb(249, 244, 219);
  padding: 9px 0;
}
</style>

