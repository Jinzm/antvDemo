<script lang="ts">
import { defineComponent } from "vue";
import { getTeleport } from "@antv/x6-vue-shape";
import { GridLayout, DagreLayout } from "@antv/layout";
const TeleportContainer = getTeleport();
export default defineComponent({
  name: "App",
  components: {
    TeleportContainer,
  },
});
</script>

<script lang="ts" setup>
import { Graph, Path, Shape } from "@antv/x6";
import {
  ref,
  onMounted,
  watch,
  computed,
  nextTick,
  onBeforeUnmount,
} from "vue";
import { MiniMap } from "@antv/x6-plugin-minimap";
import { customAlphabet } from "nanoid";
import { register } from "@antv/x6-vue-shape";
import Node from "./GraphNode.vue";

register({
  shape: "dag-node",
  width: 200,
  height: 48,
  component: Node,
});

const containerRef = ref();
const minimapRef = ref();
const graph = ref<Graph>();

const initGrapgHandler = (data = {}) => {
  let _graph = new Graph({
    panning: {
      enabled: true,
    },
    container: containerRef.value,
  });

  graph.value = _graph;

  graph.value?.fromJSON(data);
};

onMounted(() => {
  initGrapgHandler({
    cells: [
      {
        shape: "edge",
        id: "5",
        zIndex: 0,
        controlPoints: [{ x: 0, y: 69 }],
        source: { cell: "1" },
        target: { cell: "2" },
      },
      {
        position: { x: 0, y: 0 },
        size: { width: 200, height: 48 },
        view: "vue-shape-view",
        shape: "dag-node",
        id: "1",
        data: { label: "读数据", status: "success" },
        zIndex: 1,
        _order: 0,
      },
      {
        position: { x: 0, y: 138 },
        size: { width: 200, height: 48 },
        view: "vue-shape-view",
        shape: "dag-node",
        id: "2",
        data: { label: "逻辑回归", status: "success" },
        zIndex: 1,
        _order: 0,
      },
    ],
  });
});

onBeforeUnmount(() => {
  graph.value.dispose();
});
</script>
<template>
  <div class="antWrapper" style="width: 100vw">
    <div
      ref="containerRef"
      class="antCon"
      style="width: 100%; height: 100%"
    ></div>
    <TeleportContainer />
  </div>
</template>

<style lang="postcss" scoped>
.antWrapper {
  position: relative;
  min-height: 300px;
  height: 300px;

  .toolbar {
    position: absolute;
    z-index: 1;
    background-color: #fff;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: flex-end;

    img {
      width: 18px;
      height: 18px;
      opacity: 0.6;

      &:hover {
        opacity: 0.4;
      }
    }
  }

  .minimap {
    position: absolute;
    top: 20px;
    right: 20px;
  }
}

:deep(.x6-edge) {
  &:hover path:nth-child(2) {
    stroke: #1890ff;
    stroke-width: 1px;
  }
}

:deep(.x6-edge-selected) {
  path:nth-child(2) {
    stroke: #1890ff;
    stroke-width: 2px;
  }
}
</style>
