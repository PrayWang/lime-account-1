<template>
  <div>
    <layout class-prefix="layout">
      <NumberPad @update:value="onUpdateAmount" @submit="saveRecord"/>
      <div class="notes-wrapper">
        <FormItem  field-name="备注" placeholder="请输入备注" @update:value="onUpdateNotes"/>
      </div>
      <Tags :data-source.sync="tags" @update:value="onUpdateTags"/>
      <Types :value.sync="record.type"/>
    </layout>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import NumberPad from '@/components/Money/NumberPad.vue';
import Tags from '@/components/Money/Tags.vue';
import Types from '@/components/Money/Types.vue';
import {Component, Watch} from 'vue-property-decorator';
import {recordListModel} from '@/models/recordListModel';
import {tagListModel} from '@/models/tagListModel';
import FormItem from '@/components/Money/formItem.vue';

const recordList = recordListModel.fetch();

@Component({
  components: {FormItem, Types,Tags, NumberPad}
})
export default class Money extends Vue {
  tags = window.tagList;
  recordList: RecordItem[] = recordList;
  record: RecordItem = {
    tags: [], notes: '', type: '-', amount: 0
  };

  onUpdateTags(value: string[]) {
    this.record.tags = value;
  }

  onUpdateNotes(value: string) {
    this.record.notes = value;
  }

  onUpdateAmount(value: string) {
    this.record.amount = parseFloat(value);
  }

  saveRecord() {
   recordListModel.create(this.record)
  }

  @Watch('recordList')
  onRecordListChange() {
    recordListModel.save();
  }
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}

.notes-wrapper{
  border: 3px solid #25C877;
  border-radius: 10px;
  background: rgb(249, 244, 219);
  padding: 9px 0;
}
</style>

