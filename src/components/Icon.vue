<template>
  <svg class="icon">
    <use :xlink:href="'#'+name" />
  </svg>
</template>

<script lang="ts">

let importAll = (requireContext:__WebpackModuleApi.RequireContext) => requireContext.keys().forEach(requireContext);
try{
  importAll(require.context('../assets/icons',true,/\.svg$/));
}catch(error){
  console.log(error);
}
//这段代码将一个目录里同一个后缀的文件，统一引入到当前文件

export default {
  props:['name'],
  name: 'Icon'
};
</script>

<style lang="scss" scoped>
  .icon{
    width:1em;
    height: 1em;
    vertical-align: -0.15em;
    fill:currentColor;
    overflow: hidden;
  }
</style>