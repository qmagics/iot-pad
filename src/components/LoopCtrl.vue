<template>
  <div class="loop-ctrl" @click="vState=vState=='on'?'off':'on'">
    <div class="loop-code">{{code}}</div>
    <div class="loop-bar-top"></div>
    <div class="loop-bar-bottom"></div>
    <div class="loop-switch" :class="vState"></div>
    <div class="loop-states" :class="vState">
      <SvgIcon icon-class="arrow-down" />
      <span class="point"></span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    code: {},
    state: {},
    icons: {},
  },

  watch: {
    state(val) {
      this.vState = val;
    },
    vState(val) {
      this.$emit("update:state", val);
    },
  },

  data() {
    return {
      vState: this.state,
      IconMap: {
        A: "a",
        B: "v",
        C: "lightning",
        D: "temperature",
      },
    };
  },
};
</script>

<style lang="scss">
.loop-ctrl {
  $width: 0.5rem;
  $height: 1rem;
  $barWidth: 0.04rem;
  $gutter: 0.24rem;
  margin-right: 0.14rem;

  display: inline-flex;
  width: $width;
  height: $height;
  flex-direction: column;
  align-items: center;
  position: relative;
  // margin-bottom: 0rem;
  padding: 0.1rem 0;
  border-radius: 0.04rem;
  transition: background 0.15s ease;

  &:hover {
    background: rgba(26, 146, 255, 0.1);
  }

  &:before {
    top: 0.7rem;
  }
  &:after {
    top: 0.86rem;
  }

  .loop-code {
    width: 0.18rem;
    height: 0.2rem;
    color: rgba(#fff, 0.8);
    border: 0.01rem solid rgb(78, 131, 150);
    border-radius: 0.06rem;
    background: rgb(7, 21, 38);
    line-height: 0.2rem;
    text-align: center;
    font-size: 0.12rem;
    letter-spacing: -0.01rem;
  }
  .loop-bar-top,
  .loop-bar-bottom {
    background: rgb(1, 44, 86);
    border: 0.01rem solid rgb(78, 131, 150);
    border-radius: $barWidth/2;
    width: $barWidth;
  }
  .loop-bar-top {
    margin-top: 0.08rem;
    height: 0.8rem;
  }
  .loop-bar-bottom {
    margin-top: $gutter;
    height: 0.24rem;
  }
  .loop-switch {
    width: $barWidth * 2;
    height: $barWidth * 2;
    border-radius: 50%;
    background: rgb(123, 195, 255);
    position: absolute;
    top: 0.54rem;
    z-index: 1;

    &:before {
      content: "";
      width: $barWidth * 2;
      height: $barWidth * 2;
      border-radius: 50%;
      background: rgb(123, 195, 255);
      position: absolute;
      top: $gutter;
    }

    &:after {
      content: "";
      width: $barWidth;
      border-radius: $barWidth/2;
      background: rgb(123, 195, 255);
      position: absolute;
      top: 0.03rem;
      left: 0.015rem;
      height: $gutter;
      transition: all 0.2s ease;
      transform-origin: top;
    }

    &.off {
      &:after {
        transform: rotate(-45deg);
      }
    }
  }
  .loop-states {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: absolute;
    top: 0.45rem;
    padding: 0 0.06rem 0 0.04rem;
    &.off {
      .point {
        background: rgb(122, 122, 122);
      }
    }
    .svg-icon {
      font-size: 0.2rem;
    }

    .point {
      width: 0.08rem;
      height: 0.08rem;
      background: rgb(67, 255, 183);
      border-radius: 50%;
    }
  }
  .loop-icons {
    height: 1rem;
    overflow: hidden;
    margin-top: 0.02rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    .svg-icon {
      font-size: 0.16rem;
      margin-bottom: 0.02rem;
    }
  }
}
</style>