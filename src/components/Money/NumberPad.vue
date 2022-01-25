<template>
  <div class="numberPad">
    <div class="output">{{ output || '&nbsp;' }}</div>
    <div class="buttons">
      <button @click="inputContent">1</button>
      <button @click="inputContent">2</button>
      <button @click="inputContent">3</button>
      <button @click="remove"> <Icon name="remove"/></button>
      <button @click="inputContent">4</button>
      <button @click="inputContent">5</button>
      <button @click="inputContent">6</button>
      <button @click="clear"> <Icon name="clear"/></button>
      <button @click="inputContent">7</button>
      <button @click="inputContent">8</button>
      <button @click="inputContent">9</button>
      <button @click="inputContent">.</button>
      <button class="zero" @click="inputContent">0</button>
      <button class="OK" @click="OK">OK</button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

@Component
export default class NumberPad extends Vue {
  output: string = '0';

  inputContent(event: MouseEvent) {
    const button = (event.target as HTMLButtonElement);
    const input = button.textContent as string;
    if (this.output.length === 16) {return;}
    if (this.output === '0') {
      if ('0123456789'.indexOf(input) >= 0) {
        this.output = input;
      } else {
        this.output += button.textContent;
      }
      return;
    }
    if (this.output.indexOf('.') >= 0 && input === '.') {return;}
    this.output += button.textContent;
  }

  remove() {
    if (this.output.length === 1) {
      this.output = '0';
    } else {
      this.output = this.output.slice(0, -1);
    }
  }

  clear() {
    this.output = '0';
  }

  OK() {
    this.$emit('update:value', this.output);
    this.$emit('submit',this.output)
    this.output = '0';
  }

};

</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";

.numberPad {
  background: #5AD28C;

  .output {
    background: #F7F7F7;
    color: #F2A291;
    font-size: 36px;
    font-family: Consolas, monospace;
    padding: 9px 16px;
    text-align: right;
  }

  .buttons {
    @extend %clearFix;
    margin-right: -(4%);

    > button {
      float: left;
      width: 20%;
      height: 5%;
      margin: 2.5% 2%;
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
  }
}
</style>