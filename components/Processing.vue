<template>
  <div id="container"></div>
</template>

<script>
if (process.client) {
  const p5 = require('p5')
  const sketch = function(p) {
    p.setup = function() {
      p.createCanvas(500, 500)
      p.background(255)
    }
  }

  // eslint-disable-next-line no-new,new-cap
  new p5(sketch, 'container')
}
</script>
