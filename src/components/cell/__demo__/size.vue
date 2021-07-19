<template>
  <div>
    <d-cell @click="handleClick" title="单元格" value="内容" size="large"></d-cell>
    <d-cell @click="handleClick" title="单元格" value="内容" label="描述信息" size="large"></d-cell>
  </div>
  
</template>

<script>
  export default {
    methods: {
      handleClick() {
        alert('hello');
      },
    },
  };
</script>
