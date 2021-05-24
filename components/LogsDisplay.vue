<!-- eslint-disable vue/no-v-html -->
<template>
  <div class="p-4 w-100 mw-100 codeviewer">
    <code v-for="line in $props.logs" :key="line" v-html="line"></code>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  props: {
    logs: {
      type: Array,
      default: () => {
        return [''];
      },
    },
  },
});
</script>
