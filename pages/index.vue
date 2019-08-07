<template>
  <div class="container">
    <div>
      <Processing />
      <h1 class="title">
        metalnoir
      </h1>
      <h2 class="subtitle">
        Black Metal project
      </h2>
    </div>
  </div>
</template>

<script>
import Processing from '~/components/Processing.vue'

export default {
  components: {
    Processing
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #35495e;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #f5f5f5;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #f5f5f5;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
