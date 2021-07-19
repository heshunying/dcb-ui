<template>
  <div>
    <d-cell @click="handleClick" value="内容">
        <template #title>
            <span class="custom-title">单元格</span>
            <span class="custom-title">标签</span>
        </template>
    </d-cell>
    <d-cell @click="handleClick" title="单元格" icon="calendar">
        <template #right-icon>
          <d-icon name="search" class="search-icon"/>
        </template>
    </d-cell>
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

<style scoped lang="scss">
  .custom-title {
    margin-right: 4px;
    vertical-align: middle;
  }
  .search-icon {
    font-size: 16px;
    line-height: inherit;
  }
</style>