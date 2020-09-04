<template lang="html">
  <div class="headerNav container">
    <div class="header">Digital Xylophone</div>
  </div>
</template>

<script>
  export default {
    mounted() {
      console.log('New component mounted.')
    }
  }
</script>

<style lang="css">
.headerNav {
  margin-bottom: 60px;
  text-align: left;
}

.header {
  font-size: 3em;
  font-family: monospace;
  color: green;
}
</style>
