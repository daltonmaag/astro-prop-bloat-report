<script setup lang="ts">
import { onMounted, ref } from "vue";

const props = defineProps({
  nesting: { type: Number, required: true },
  data: { type: Object, required: true },
});

const json = JSON.stringify(props.data);

const propBytes = json.length;

const astroPropBytes = ref(0);

const root = ref<HTMLDivElement | null>(null);
onMounted(() => {
  astroPropBytes.value =
    root.value?.parentElement?.getAttribute("props")?.length ?? 0;
});
</script>

<template>
  <div ref="root">
    <span>Nesting {{ nesting }}</span>
    <span>JSON bytes {{ propBytes }}</span>
    <span>Astro bytes {{ astroPropBytes }}</span>
    <span class="json">JSON: {{ json }}</span>
  </div>
</template>

<style scoped>
div {
  display: flex;
  border-bottom: 1px solid grey;
}
span {
  width: 10rem;
}
.json {
  width: max-content;
}
</style>
