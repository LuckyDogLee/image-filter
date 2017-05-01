<template>
  <div id="image-edit">
    <!-- <div id="image-container">
      <img id="image" :src="imageDataURL">
    </div> -->
    <image-frame :dataUrl="dataUrl"></image-frame>
    <filter-gallery :dataUrl="dataUrl" :setDataUrl="setDataUrl"></filter-gallery>
    <canvas id="canvas"></canvas>
  </div>
</template>

<script>
  import FilterGallery from '../components/FilterGallery.vue';
  import ImageFrame from '../components/ImageFrame.vue';

  export default {
    name: 'image-edit',
    components: {
      'image-frame': ImageFrame,
      'filter-gallery': FilterGallery,
    },
    props: ['dataUrl', 'setDataUrl'],
  };
</script>

<style>
  #image-edit {
    position: relative;
    width: 100%;
    height: 100%;
    background-color: #333;
    overflow: hidden;
  }

  #image-frame {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 130px;
    left: 0;
  }

  #filter-gallery {
    position: absolute;
    bottom: 0;
    height: 130px;
  }
</style>
