<template>
 <div>
   <layout class-prefix="layout">
     <NumberPad />
     <Notes />
     <Tags :data-source="tags"/>
     <Types />
   </layout>
 </div>
</template>

<script lang="js">
import NumberPad from '@/components/Money/NumberPad.vue';
import Tags from '@/components/Money/Tags.vue';
import Notes from '@/components/Money/Notes.vue';
import Types from '@/components/Money/Types.vue';
export default {
  name: 'Money',
  components: {Types, Notes, Tags, NumberPad},
  data(){
    return{
      tags:['衣','食','住','行']
    }
  }
};
</script>

<style lang="scss">
  .layout-content{
    display: flex;
    flex-direction: column-reverse;
 }
</style>

