<script setup lang="ts">
import { defineProps } from 'vue'

defineProps<{
  link: string
}>()
</script>

<template>
  <div class="px-2 -mx-2 mt-4 py-2">
    <!-- <ri-external-link-line class="opacity-50 h-1em -mb-0.5 mr-2 inline-block" /> -->
    <span class="opacity-50">File Reference: </span><a class="font-mono opacity-75 hover:opacity-100" :href="`${link}`">{{ link.split('/main/')[1] }}</a>
  </div>
</template>
