<template>
  <div id="container"></div>
</template>
<script>
export default {
  data() {
    return {
      map: null,
    };
  },
  mounted() {
    let _this = this;
    _this.map = new BMapGL.Map("container");
    var point = new BMapGL.Point(110.331019,20.033487);
    _this.map.centerAndZoom(point, 11);
    _this.map.enableScrollWheelZoom(true); //启用滚轮放大缩小，默认禁用
    _this.map.enableKeyboard(true); //启用键盘操作，默认禁用。
    _this.map.enableDragging(); //启用地图拖拽，默认启用
    _this.map.enableDoubleClickZoom(); //启用双击放大，默认启用
    _this.map.addControl(new BMapGL.ScaleControl()); //比例尺控件
    _this.map.setMapStyleV2({ styleJson: styleJson2 });
    var options = {
      onSearchComplete: function (results) {
        if (driving.getStatus() == BMAP_STATUS_SUCCESS) {
          let a = results.getNumPlans();
          debugger
          // // 获取第一条方案
          // var plan = results.getPlan(0);
          // // 获取方案的驾车线路
          // var route = plan.getRoute(0);
          // // 获取每个关键步骤，并输出到页面
          // var s = [];
          // for (var i = 0; i < route.getNumSteps(); i++) {
          //   var step = route.getStep(i);
          //   console.log(step);
          // }
          // 地图覆盖物
          _this.addOverlays(results);
          // 方案描述
          // _this.addText(results);
        }
      },
    };
    var driving = new BMapGL.DrivingRoute(_this.map, options);
    // var start = "海怡豪园";
    // var end = "国贸大厦";
    var start = new BMapGL.Point(110.331019, 20.033487);
    var end = new BMapGL.Point(110.306304, 20.030096);
    driving.search(start, end);
  },
  methods: {
    // 添加覆盖物并设置视野
    addOverlays(results) {
      // 自行添加起点和终点
      var start = results.getStart();
      var end = results.getEnd();
      this.addStart(start.point, start.title);
      this.addEnd(end.point, end.title);
      var viewPoints = [start.point, end.point];
      // 获取方案
      var plan = results.getPlan(0);
      // 获取方案中包含的路线
      for (var i = 0; i < plan.getNumRoutes(); i++) {
        this.addRoute(plan.getRoute(i).getPath());
        viewPoints.concat(plan.getRoute(i).getPath());
      }
      // 设置地图视野
      this.map.setViewport(viewPoints, {
        margins: [40, 10, 10, 10],
      });
    },
    // 添加方案描述
    addText(results) {
      var plan = results.getPlan(0);
      // 获取方案中包含的路线
      var htmls = [];
      for (var i = 0; i < plan.getNumRoutes(); i++) {
        var route = plan.getRoute(i);
        for (var j = 0; j < route.getNumSteps(); j++) {
          var curStep = route.getStep(j);
          htmls.push(j + 1 + ". " + curStep.getDescription() + "<br />");
        }
      }
      var panel = document.getElementById("panel");
      panel.innerHTML = htmls.join("");
      panel.style.lineHeight = "1.4em";
      panel.style.fontSize = "12px";
    },
    // 添加起点覆盖物
    addStart(point, title) {
      this.map.addOverlay(
        new BMapGL.Marker(point, {
          title: title,
          icon: new BMapGL.Icon("blue.png", new BMapGL.Size(38, 41), {
            anchor: new BMapGL.Size(4, 36),
          }),
        })
      );
    },
    // 添加终点覆盖物
    addEnd(point, title) {
      this.map.addOverlay(
        new BMapGL.Marker(point, {
          title: title,
          icon: new BMapGL.Icon("red.png", new BMapGL.Size(38, 41), {
            anchor: new BMapGL.Size(4, 36),
          }),
        })
      );
    },
    // 添加路线
    addRoute(path) {
      this.map.addOverlay(
        new BMapGL.Polyline(path, {
          strokeColor: "green",
          enableClicking: false,
        })
      );
    },
  },
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