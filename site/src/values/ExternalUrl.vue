<template>
  <a
    :href="url"
    target="_blank"
    class="whitespace-nowrap"
    rel="noopener noreferrer">
    {{ renderedText }}
    <icon
      icon="external-link"
      size="small" />
  </a>
</template>

<script lang="ts" setup>
  import {computed} from "vue";
  import type * as t from "@/logic/types";

  const properties = defineProps<{url: t.URL; text?: string | null}>();

  const renderedText = computed(() => {
    if (properties.text) {
      return properties.text;
    }

    return properties.url;
  });
</script>

<style></style>
