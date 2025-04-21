<!--  -->
<script lang='ts' setup>
import { ref } from 'vue'

const props = defineProps({
  node: Object,
  graph: Object
})

const label = ref(props.node.data.label)

</script>
<template>
  <div class="node">
    <div class="label">
        {{ label }}
    </div>
  </div>
</template>

<style lang='postcss' scoped>
.node {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  height: 100%;
  background-color: #fff;
  border: 1px solid #c2c8d5;
  border-left: 4px solid #5F95FF;
  border-radius: 4px;
  box-shadow: 0 2px 5px 1px rgba(0, 0, 0, 0.06);
  padding: 0 8px;
  overflow: hidden;

  .label {
    display: inline-block;
    flex-shrink: 0;
    color: #666;
    font-size: 12px;
    overflow: hidden;
    flex: 1;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
}
</style>