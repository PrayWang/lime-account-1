<template>
  <div class="numberPad">
    <div class="output">100</div>
    <div class="buttons">
      <button class="one">1</button>
      <button class="two">2</button>
      <button class="tree">3</button>
      <button class="delete">删除</button>
      <button>4</button>
      <button>5</button>
      <button>6</button>
      <button>清空</button>
      <button>7</button>
      <button>8</button>
      <button>9</button>
      <button>.</button>
      <button class="zero">0</button>
      <button class="OK">OK</button>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'NumberPad'
};
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";
.numberPad{
  background:#5AD28C;
  .output{
    background:#F7F7F7;
    color: #F2A291;
    font-size:36px;
    font-family: Consolas,monospace;
    padding: 9px 16px;
    text-align: right;
  }
  .buttons {
    @extend %clearFix;
    margin-right: -(4%);

    > button {
      float: left;
      width: 20%;
      height: 46px;
      margin-right: 2%;
      margin-left: 2%;
      margin-top: 2.5%;
      margin-bottom: 2.5%;
      background: #F7F7F7;
      border-radius: 10px;
      box-shadow: 2px 2px 2px 2px rgba(0, 0, 0, .2);
      border: none;
      font-size: 24px;
      text-align: center;
      color: #25C877;

      &.OK {
        margin-right: 2%;
        width: 44%;
        background: #FEF3BB;
      }

      &.zero {
        margin-right: 2%;
        width: 44%;
      }

    }
  }}
</style>