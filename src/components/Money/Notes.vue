<template>
  <div>
    <label class="notes">
      <span class="name">备注</span>
      <input type="text" placeholder="在这里输入备注">
    </label>
  </div>
</template>

<script lang="ts">
export default {
  name: 'Notes'
};
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";
.notes{
  border: 2px solid #25C877;
  border-radius: 10px;
  font-size: 14px;
  background: rgb(249,244,219);
  display: flex;
  padding-left: 16px;
  align-items: center;
  .name{
    padding-right: 16px;
  }
  input{
    height: 62px;
    flex-grow: 1;
    background: transparent;
    border: none;
    padding-right: 16px;
  }
}
</style>