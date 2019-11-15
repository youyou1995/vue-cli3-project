<template>
    <div class="about">
        <h1>This is an about page</h1>
        <div class="about_img">
            <img src="https://upload-images.jianshu.io/upload_images/2259045-d35ccfb2170e99e2?imageMogr2/auto-orient/strip|imageView2/2/format/webp"
                 alt="">
            <canvas class="qrcode" ref="qrcode"></canvas>
        </div>
        <banner-qrcode
                banner-path="https://upload-images.jianshu.io/upload_images/2259045-d35ccfb2170e99e2?imageMogr2/auto-orient/strip|imageView2/2/format/webp"
                :banner-width="400" :banner-height="500" :position-x="100" :position-y="100"
                path="https://www.baidu.com" :size="120"
        ></banner-qrcode>
    </div>
</template>

<script>
  import Qrious from 'qrious';
  import BannerQrcode from "../components/BannerQrcode";

  export default {
    data() {
      return {
        qrious: null
      };
    },
    components: {BannerQrcode},
    methods: {
      markQrcode() {
        const element = this.$refs.qrcode;
        this.qrious = new Qrious({
          element,
          value: 'https://www.baidu.com',
          background: 'green', //颜色
          backgroundAlpha: 0.2,
          foreground: 'red',
          foregroundAlpha: 0.8,
          level: 'H',
          // padding: 25,
          size: 100,
        });
        console.log('qrious', this.qrious);
      }
    },
    mounted() {
      this.markQrcode();
      console.log('qrcode');
    }
  };
</script>

<style lang="scss">
    .about {
        .about_img {
            width: 400px;
            height: 400px;
            position: relative;
            margin: 0 auto;

            > img {
                width: 100%;
            }

            .qrcode {
                position: absolute;
                bottom: 120px;
                right: 20px;
                width: 200px;
                height: 200px;
                margin: 0 auto;
                background-color: #42b983;
            }
        }
    }
</style>
