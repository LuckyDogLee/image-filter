<template>
  <div id="app">
    <camera v-if="shoot" :setDataUrl="setDataUrl"></camera>
    <image-edit v-else :dataUrl="imageDataUrl" :setDataUrl="setDataUrl"></image-edit>
  </div>
</template>

<script>
  import Camera from './pages/Camera.vue';
  import ImageEdit from './pages/ImageEdit.vue';

  export default {
    name: 'app',
    components: {
      camera: Camera,
      'image-edit': ImageEdit,
    },
    data() {
      return {
        shoot: true,
        imageDataUrl: '',
      };
    },
    // computed: {
    //   dataUrl() {
    //     let dataUrl = '';
    //     if (shoot === false) {
    //       dataUrl = this.imgDataUrl;
    //     }
    //     return dataUrl;
    //   },
    // },
    methods: {
      setDataUrl(imgDataUrl) {
        this.imageDataUrl = imgDataUrl;
        this.shoot = false;
      },
    },
  };
</script>

<style>
  html {
    font-size: 12px;
    font-family: sans-serif;
  }

  html,
  body,
  #app {
    width: 100%;
    height: 100%;
  }

  body {
    margin: 0;
    box-sizing: border-box;
  }

  h1 {
    text-align: center;
  }

  a {
    color: black;
    text-decoration: none;
  }

  ul {
    padding: 0;
    margin: 0;
    list-style: none;  
  }

  #app {
    color: #fff;
  }

  #image-container {
    display: flex;
    align-items: center;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 130px;
    left: 0;
  }

  #image {
    width: 100%;
  }

  #filter-gallery {
    position: fixed;
    bottom: 0;
    height: 130px;
  }
</style>
