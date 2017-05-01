<template>
  <ul id="filter-gallery">
    <li>
      <img :style="{ backgroundImage: `url(${dataUrl0})` }" :class="{ active: index === 0 }" @click="change(dataUrl0, 0)" />
      <span>无</span>
    </li>
    <li>
      <img :style="{ backgroundImage: `url(${dataUrl1})` }" :class="{ active: index === 1 }" @click="change(dataUrl1, 1)" />
      <span>冲印</span>
    </li>
    <li>
      <img :style="{ backgroundImage: `url(${dataUrl2})` }"  :class="{ active: index === 2 }" @click="change(dataUrl2, 2)" />
      <span>反色</span>
    </li>
    <li>
      <img />
      <span>黑白</span>
    </li>
    <li>
      <img />
      <span>岁月</span>
    </li>
    <li>
      <img />
      <span>浮雕</span>
    </li>
  </ul>
</template>

<script>
  export default {
    name: 'filter-gallery',
    props: ['dataUrl', 'setDataUrl'],
    data() {
      return {
        dataUrl0: '',
        dataUrl1: '',
        dataUrl2: '',
        index: 0,
      };
    },
    methods: {
      change(dataUrl, index) {
        this.setDataUrl(dataUrl);
        this.index = index;
      },
    },
    created() {
      let width;
      let height;
      this.dataUrl0 = this.dataUrl;
      const img = new Image();
      img.src = this.dataUrl;
      img.onload = () => {
        width = img.width;
        height = img.height;
        if (width > 2000) {
          width /= 5;
          height /= 5;
        } else if (width > 1600) {
          width /= 4;
          height /= 4;
        } else if (width > 1200) {
          width /= 3;
          height /= 3;
        } else if (width > 800) {
          width /= 2;
          height /= 2;
        }
        const canvas = document.getElementById('canvas');
        canvas.width = width;
        canvas.height = height;
        const ctx = canvas.getContext('2d');
        ctx.drawImage(img, 0, 0, width, height);
        const originImageData = ctx.getImageData(0, 0, width, height);
        originImageData.data.forEach((item, index, data) => {
          const temp = index + 1;
          if ((temp - 3) % 4 !== 0) { return; }
          const r = data[index - 2];
          const g = data[index - 1];
          const b = data[index];
          data[index - 2] = (r * 0.272) + (g * 0.534) + (b * 0.131);
          data[index - 1] = (r * 0.349) + (g * 0.686) + (b * 0.168);
          data[index] = (r * 0.393) + (g * 0.769) + (b * 0.189);
        });
        ctx.putImageData(originImageData, 0, 0);
        this.dataUrl1 = canvas.toDataURL();
      };

      const img2 = new Image();
      img2.src = this.dataUrl;
      img2.onload = () => {
        const canvas2 = document.getElementById('canvas');
        const ctx2 = canvas2.getContext('2d');
        ctx2.drawImage(img, 0, 0, width, height);
        const originImageData2 = ctx2.getImageData(0, 0, width, height);
        originImageData2.data.forEach((item, index, data) => {
          if ((index + 1) % 4 === 0) { return; }
          data[index] = 255 - item;
        });

        ctx2.putImageData(originImageData2, 0, 0);
        this.dataUrl2 = canvas.toDataURL();
      };
    },
  };
</script>

<style>
  #filter-gallery,
  #filter-gallery li {
    box-sizing: border-box;
  }

  #filter-gallery {
    width: 100%;
    white-space: nowrap;
    overflow-x: auto;
    overflow-y: hidden;
    background-color: #333;
  }

  #filter-gallery li {
    display: inline-block;
  }

  #filter-gallery li img {
    display: block;
    width: 100px;
    height: 100px;
    border: 1px solid black;
    box-sizing: border-box;
    background-size: 100px auto;
    background-position: center;
    background-repeat: no-repeat;
  }

  #filter-gallery li img.active {
    border: 3px solid #3c9bf5;
  }

  #filter-gallery li span {
    display: inline-block;
    width: 100px;
    font-size: 15px;
    padding: 5px 0;
    text-align: center;
    color: inherit;
  }

  #canvas {
    position: absolute;
    z-index: -1;
  }
</style>
