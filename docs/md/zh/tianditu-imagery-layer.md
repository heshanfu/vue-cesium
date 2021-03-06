<template lang="markdown">

# 天地图服务图层

`TiandituImageryLayer`

## 属性

|属性名|类型|默认值|描述|
|------|-----|-----|----|
|mapStyle|String|'img_w'|`optional`指定天地图服务类型。|
|rectangle|Cesium.Rectangle||`optional`图层的矩形范围,此矩形限制了影像可见范围。|
|alpha|Number\|function|1.0|`optional`图层透明度值，取值范围为0.0~1.0。|
|brightness|Number\|function|1.0|`optional`图层亮度值。值为1.0表示使用原图；值大于1.0时图像将变亮；值小于1.0时图像将变暗。|
|contrast|Number\|function|1.0|`optional`图层对比度。值为1.0表示使用原图；值大于1.0表示增加对比度；值小于1.0表示降低对比度。|
|hue|Number\|function|0.0|`optional`图层色调。值为0.0表示使用原图。|
|saturation|Number\|function|1.0|`optional`图层饱和度。值为1.0表示使用原图；值大于1.0表示增加饱和度；值小于1.0表示降低饱和度。|
|gamma|Number\|function|1.0|`optional`图层伽马校正。值为1.0表示使用原图。|
|show|Boolean|true|`optional`指定图层是否显示，true表示显示此图层，false表示不显示。|
|splitDirection|Number||`optional`指定影像图层分割方向。0始终显示影像图层，-1在Scene#imagerySplitPosition的左侧显示影像图层，1在Scene#imagerySplitPosition右侧显示影像图层。|
|minimumTerrainLevel|Number||`optional`最小地形细节层次。level 0是最小细节层次。|
|maximumTerrainLevel|Number||`optional`最大地形细节层次。|

## 事件

|事件名|参数|描述|
|------|----|----|
|ready|{Cesium, viewer, originInstance}|返回Cesium类, viewer实例, 以及添加的图层对象originInstance, 也就是ImageryLayer。|

## 示例

### 天地图服务图层

#### 代码

```html
<template>
  <div class="viewer">
    <div style="position: absolute; left: 1%; top: 1%; width: 150px; z-index: 9999; color: white">
      <span>透明度</span>
      <el-slider v-model="alpha" :min="0" :max="1" :step="0.01" ></el-slider>
      <span>亮度</span>
      <el-slider v-model="brightness" :min="0" :max="3" :step="0.01" ></el-slider>
      <span>对比度</span>
      <el-slider v-model="contrast" :min="0" :max="3" :step="0.01" ></el-slider>
      <span>切换服务</span>
      <el-select v-model="mapStyle" placeholder="请选择服务">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value">
        </el-option>
      </el-select>
    </div>
    <cesium-viewer>
      <tianditu-imagery-layer :mapStyle="mapStyle" :alpha="alpha" :brightness="brightness" 
      :contrast="contrast" @ready="ready" />
    </cesium-viewer>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        options: [{
          value: 'img_c',
          label: '天地图全球影像地图服务（经纬度投影）'
        }, {
          value: 'vec_c',
          label: '天地图全球矢量地图服务（经纬度投影）'
        }],
        mapStyle: 'vec_c',
        alpha: 1,
        brightness: 1,
        contrast: 1
      }
    },
    methods: {
      ready (cesiumInstance) {
        const {Cesium, viewer, originInstance} = cesiumInstance
        // viewer.zoomTo(originInstance)
      }
    }
  }
</script>

<style>
.viewer {
  width: 100%;
  height: 400px;
}
</style>
```

#### 预览

<doc-preview>
  <template>
    <div class="viewer">
      <div style="position: absolute; left: 1%; top: 1%; width: 150px; z-index: 9999; color: white">
        <span>透明度</span>
        <el-slider v-model="alpha" :min="0" :max="1" :step="0.01" ></el-slider>
        <span>亮度</span>
        <el-slider v-model="brightness" :min="0" :max="3" :step="0.01" ></el-slider>
        <span>对比度</span>
        <el-slider v-model="contrast" :min="0" :max="3" :step="0.01" ></el-slider>
        <span>切换服务</span>
        <el-select v-model="mapStyle" placeholder="请选择服务">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
      </div>
      <cesium-viewer>
        <tianditu-imagery-layer :mapStyle="mapStyle" :alpha="alpha" :brightness="brightness" 
        :contrast="contrast" @ready="ready" />
      </cesium-viewer>
    </div>
  </template>

  <script>
    export default {
      data () {
        return {
          options: [{
            value: 'img_c',
            label: '天地图全球影像地图服务（经纬度投影）'
          }, {
            value: 'vec_c',
            label: '天地图全球矢量地图服务（经纬度投影）'
          }],
          mapStyle: 'vec_c',
          alpha: 1,
          brightness: 1,
          contrast: 1
        }
      },
      methods: {
        ready (cesiumInstance) {
          const {Cesium, viewer, originInstance} = cesiumInstance
          // viewer.zoomTo(originInstance)
        }
      }
    }
  </script>

  <style scoped>
  .viewer {
    width: 100%;
    height: 400px;
  }
  </style>
</doc-preview>