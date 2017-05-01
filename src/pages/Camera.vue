<template>
  <div id="camera">
    <div class="capture-wrapper">
      <input id="real-capture" class="real" type="file" capture="user" accept="image/*" @change="getImageDataUrl('real-capture')" />
      <a class="capture">相机</a>
    </div>
    <div class="capture-wrapper">
      <input id="real-photos" class="real" type="file" @change="getImageDataUrl('real-photos')" />
      <a class="capture">相册</a>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'camera',
    props: ['setDataUrl'],
    methods: {
      getImageDataUrl(id) {
        const camera = document.getElementById(id);
        const images = camera.files;
        if (images.length === 0) { return; }
        const image = images[0];
        const imageReader = new FileReader();
        imageReader.onload = (event) => {
          const imgDataUrl = event.target.result;
          this.setDataUrl(imgDataUrl);
        };
        imageReader.readAsDataURL(image);
      },
    },
  };
</script>

<style>
  #camera {
    display: flex;
    justify-content: space-around;
    align-items: flex-end;
    box-sizing: border-box;
    padding-bottom: 20px;
    width: 100%;
    height: 100%;
    background-color: #f4f4f4;
  }

  .capture-wrapper {
    position: relative;
  }

  .real {
    position: absolute;
    opacity: 0;
    width: 60px;
    height: 60px;
    z-index: 2;
  }

  .capture {
    display: table-cell;
    text-align: center;
    vertical-align: middle;
    width: 60px;
    height: 60px;
    background-color: rgba(0, 0, 0, .3);
    border-radius: 50%;
    color: white;
    z-index: 1;
  }
</style>
