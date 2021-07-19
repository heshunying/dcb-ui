<template>
  <div class="link">
    <d-cell @click="handleClick" title="单元格" is-link ></d-cell>
    <d-cell @click="handleClick" title="单元格" value="内容" is-link ></d-cell>
  </div>
  
</template>

<script>
  export default {
    data(){
        return{
            url:'https://marriage-photo-collect-test.oss-cn-gz-ysgzlt-d01-a.ltops.gzdata.com.cn/marriage-photo-collect-test/68306b0cf96246ceb4ce31ac0c6b1a5f.jpg'
        }
    },
    methods: {
      handleClick() {
        alert('hello');
      },
    },
  };
</script>

<style lang="scss">
    .link{
        .d-icon{
            transform: rotate(180deg);
        }
    }
    
</style>
