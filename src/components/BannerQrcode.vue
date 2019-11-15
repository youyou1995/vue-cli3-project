<template>
    <div class="banner_qr_code">
        <div class="banner" :style="{width: `${bannerWidth}px`,height: `${bannerHeight}px`}">
            <img :src="bannerPath" alt="banner图">
            <canvas class="qrcode" ref="qrcode" :style="{left: `${positionX}px`, top: `${positionY}px`}"></canvas>
        </div>
    </div>
</template>

<script>
  import Qrious from 'qrious';

  export default {
    name: "BannerQrcode",
    props: {
      // banner图地址
      bannerPath: {
        type: String,
        required: true
      },
      bannerWidth: {
        type: Number,
        required: true
      },
      bannerHeight: {
        type: Number,
        required: true
      },
      // 二维码x距离
      positionX: {
        type: Number,
        required: true
      },
      // 二维码y距离
      positionY: {
        type: Number,
        required: true
      },
      // 商品路径
      path: {
        type: String,
        required: true
      },
      // 二维码背景色
      backgroundColor: {
        type: String,
        default: '#fff'
      },
      // 二维码背景透明度
      backgroundAlpha: {
        type: Number,
        default: 0.8
      },
      // 二维码颜色
      foregroundColor: {
        type: String,
        default: '#000'
      },
      // 二维码透明度
      foregroundAlpha: {
        type: Number,
        default: 0.8
      },
      // 二维码纠错等级
      level: {
        type: String,
        default: 'H',
        validator(value) {
          return ['L', 'M', 'Q', 'H'].indexOf(value) !== -1;
        }
      },
      // 二维码大小(像素)
      size: {
        type: Number,
        default: 100
      }
    },
    methods: {
      // 生成二维码
      markQrcode() {
        const element = this.$refs.qrcode;
        this.qrious = new Qrious({
          element,
          value: this.path,
          background: this.backgroundColor,
          backgroundAlpha: this.backgroundAlpha,
          foreground: this.foregroundColor,
          foregroundAlpha: this.foregroundAlpha,
          level: this.level,
          size: this.size,
        });
      }
    },
    mounted() {
      this.markQrcode();
    }
  };
</script>

<style scoped lang="scss">
    .banner_qr_code {
        > .banner {
            width: 400px;
            height: 400px;
            position: relative;
            margin: 0 auto;

            > img {
                width: 100%;
            }

            > .qrcode {
                position: absolute;
                bottom: 120px;
                right: 20px;
            }
        }
    }
</style>
