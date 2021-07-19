<template>
  <div>
    <d-cell @click="handleClick" value="内容"></d-cell>
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
