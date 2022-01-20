<template>
 <div>
   <layout>
     <div>
       <ul class="types">
         <li class="selected pay">支出</li>
         <li class="income">收入</li>
       </ul>
     </div>
     <div class="tags">
       <ul class="current">
         <li>衣</li>
         <li>食</li>
         <li>住</li>
         <li>行</li>
       </ul>
       <div class="new">
         <button>新增标签</button>
       </div>
     </div>
     <div>
       <label class="notes">
         <span class="name">备注</span>
       <input type="text" placeholder="在这里输入备注">
       </label>
     </div>
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
   </layout>
 </div>
</template>

<script lang="ts">
export default {
  name: 'Money',
};
</script>

<style lang="scss" scoped>
  @import "~@/assets/style/helper.scss";
  .types{
    display: flex;
    text-align: center;
    font-size: 24px;
    color:azure;
    background: #5AD28C;
    >li{
      width: 50%;
      height: 64px;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
      &.selected{
        background: #25C877;
      }
      &.selected::after{
        content: '';
        position: absolute;
        bottom:0;
        left: 0;
        width: 100%;
        height: 4px;
        background: #F2A291;
      }
    }
  }
  .tags{
    font-size:14px;
    padding: 16px;
    background:#F7F7F7;
    > .current{
      display: flex;
      > li{
        background: #78C88C;
        $h:24px;
        height: $h;
        line-height: $h;
        border-radius: $h/2;
        padding: 0 16px;
        margin-right: 12px;
        color: azure;
      }
    }
    > .new{
      padding-top: 16px;
      button{
        background: transparent;
        border:none;
        color:#999999;
        border-bottom: 1px solid;
        padding: 0 4px;
      }
    }
  }
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
    .buttons{
      @extend %clearFix;
      margin-right: -(4%);
      > button{
       float: left;
        width:20%;
        height: 46px;
        margin-right: 2%;
        margin-left: 2%;
        margin-top:2.5%;
        margin-bottom: 2.5%;
        background:#F7F7F7;
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
          //margin-bottom: 5%;
        }
        &.zero {
          margin-right: 2%;
          width:44%;
          //margin-bottom: 5%;
        }
        //&.one,&.two,&.tree,&.delete{
        //  margin-top:5%;
        //}
      }
    }
  }
</style>
