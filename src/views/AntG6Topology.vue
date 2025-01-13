<template>
  <div ref="container" class="topology-container"></div>
</template>

<script setup>
import { Graph } from '@antv/g6';
import {ref} from "vue";

const container = ref(null);

const data = {
  nodes: [
    { id: 'kspacey', data: { label: 'Kevin Spacey', width: 144, height: 100 } },
    { id: 'swilliams', data: { label: 'Saul Williams', width: 160, height: 100 } },
    { id: 'bpitt', data: { label: 'Brad Pitt', width: 108, height: 100 } },
    { id: 'hford', data: { label: 'Harrison Ford', width: 168, height: 100 } },
    { id: 'lwilson', data: { label: 'Luke Wilson', width: 144, height: 100 } },
    { id: 'kbacon', data: { label: 'Kevin Bacon', width: 121, height: 100 } },
  ],
  edges: [
    { id: 'kspacey->swilliams', source: 'kspacey', target: 'swilliams' },
    { id: 'swilliams->kbacon', source: 'swilliams', target: 'kbacon' },
    { id: 'bpitt->kbacon', source: 'bpitt', target: 'kbacon' },
    { id: 'hford->lwilson', source: 'hford', target: 'lwilson' },
    { id: 'lwilson->kbacon', source: 'lwilson', target: 'kbacon' },
  ],
};

const graph = new Graph({
  autoFit: 'center',
  container: container,
  data,
  node: {
    type: 'rect',
    style: {
      size: (d) => [d.data.width, d.data.height],
      radius: 10,
      iconText: (d) => d.data.label,
      iconFontSize: 14,
    },
    palette: {
      type: 'group',
      field: 'label',
    },
  },
  edge: {
    type: 'polyline',
    style: {
      router: {
        type: 'orth',
      },
    },
  },
  layout: {
    type: 'dagre',
  },
});

graph.render();
</script>

<style scoped>
.topology-container {
  width: 100%;
  height: 100vh;
  background-color: #f4f4f4;
  position: relative;
}
</style>
