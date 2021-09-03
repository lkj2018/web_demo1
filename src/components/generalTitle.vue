<template>
  <div class="general-title" :style="{ marginTop: marginTop }">
    <div class="general-title-line">
      <div class="c-flex c-justify-between c-items-center">
        <div class="general-title-line-font">
          {{ generalTitle }}
          <span class="general-title-line-font_subtitle">{{
            generalSubTitle
          }}</span>
        </div>
        <slot name="right"></slot>
      </div>
      <div class="line"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "generalTitle",
  props: {
    generalTitle: {
      type: String,
      default: "",
    },
    generalSubTitle: {
      type: String,
      default: "",
    },
    marginTop: {
      type: String,
      default: "0",
    },
  },
};
</script>

<style scoped lang="scss">
.general-title {
  margin: 0 5px;

  &-line {
    &-font {
      font-size: 16px;
      text-shadow: 0 0 10px #2fcdff;
      color: #fff;
      width: 106px;
      line-height: 28px;
      display: inline-block;
      border-width: 0 4px 4px 0;
      border-style: none solid solid;
      border-color: transparent transparent #2fcdff;
      white-space: nowrap;
      text-overflow: ellipsis;
      &_subtitle {
        font-size: 12px;
        font-style: italic;
        line-height: 12px;
      }
    }
    .line {
      height: 0;
      border-top: 1px solid #4e5d6a;
      position: relative;
      top: -1px;
    }
  }
}
</style>
