<template>
  <div id="map" class="map_x"></div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { Map, View } from "ol";
import XYZ from "ol/source/XYZ";
import Tile from "ol/layer/Tile"; // 瓦片渲染方法
import "ol/ol.css"; // 地图样式

onMounted(() => {
  initMap();
});

// 存放地图实例
const map = ref(null);

function initMap() {
  map.value = new Map({
    target: "map",
    layers: [
      new Tile({
        source: new XYZ({
          url: "http://webst0{1-4}.is.autonavi.com/appmaptile?style=7&x={x}&y={y}&z={z}&lang=zh_cn&scale=1&size=1",
          // 高德地图的瓦片服务可能有不同的 URL 格式和参数，这里是一个示例
        }),
      }),
    ],

    view: new View({
      // 地图视图
      projection: "EPSG:4326", // 坐标系，有EPSG:4326和EPSG:3857
      center: [114.064839, 22.548857], // 深圳坐标
      minZoom: 10, // 地图缩放最小级别
      zoom: 12, // 地图缩放级别（打开页面时默认级别）
    }),
  });
}
</script>

<style>
.map_x {
  width: 100%;
  height: 600px;
  border: 1px solid #eee;
}
</style>
