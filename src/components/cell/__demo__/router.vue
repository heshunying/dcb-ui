<template>
  <div class="router">
    <d-cell @click="handleClick" title="URL跳转" url="https://baidu.com" :replace="false" is-link></d-cell>
    <d-cell @click="handleClick" title="路由跳转" to='' is-link></d-cell>
  </div>
  
</template>

<script>
  export default {
    methods: {
      handleClick() {
        // alert('hello');
      },
    },
  };
</script>

<style lang="scss">
    .router{
        .d-icon{
            transform: rotate(180deg);
        }
    }
    
</style>