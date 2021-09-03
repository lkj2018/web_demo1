<template>
  <div id="container"></div>
</template>
<script>
export default {
  data() {
    return {};
  },
  mounted() {
    var map = new BMapGL.Map("container");
    var point = new BMapGL.Point(110.280023,20.008519);
    map.centerAndZoom(point, 18);
    map.enableScrollWheelZoom(true); //启用滚轮放大缩小，默认禁用
    map.enableKeyboard(true); //启用键盘操作，默认禁用。
    map.enableDragging(); //启用地图拖拽，默认启用
    map.enableDoubleClickZoom(); //启用双击放大，默认启用
    map.addControl(new BMapGL.ScaleControl()); //比例尺控件
    map.setMapStyleV2({ styleJson: styleJson2 });
  },
  methods: {},
};
</script>
<style>
#container {
  width: 100%;
  height: 100%;
}

/* 去除百度地图版权那行字 和 百度logo */
#container > .BMap_cpyCtrl {
  display: none !important;
}
#container > .anchorBL {
  display: none !important;
}
</style>