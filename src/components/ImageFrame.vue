<template>
  <div id="image-frame">
    <img id="image" :src="dataUrl">
  </div>
</template>

<script>
  export default {
    name: 'image-frame',
    props: ['dataUrl'],
  };
</script>

<style>
  #image-frame {
    display: flex;
    align-items: center;
  }

  #image {
    width: 100%;
  }
</style>
