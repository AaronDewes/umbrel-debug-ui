<template>
  <div
    class="
      d-flex
      flex-column
      align-items-center
      justify-content-center
      h-100
      p-2
    "
  >
    <img alt="Umbrel" src="@/assets/logo.svg" class="mb-5 logo" />
    <span class="text-muted w-75 text-center">
      <small>We host debug logs of users on this server.</small>
    </span>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import 'bootstrap/dist/css/bootstrap.min.css';

export default Vue.extend({});
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
