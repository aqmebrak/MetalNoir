<template>
  <div id="container"></div>
</template>

<script>
export default {
  layout: 'default'
}
if (process.client) {
  const p5 = require('p5')
  const sketch = function(p) {
    p.setup = function() {
      p.createCanvas(window.innerWidth, window.innerHeight)
      p.background(0)
      // p.noLoop()
      p.frameRate(10)
    }

    p.draw = function() {
      p.background(0)
      // const treesAngle = 20
      p.strokeWeight(3)
      const lines = []

      for (let i = 0; i <= 50; i++) {
        const x = p.random(0, window.innerWidth)
        const y = p.random(500, window.innerHeight)
        lines.push({ x, y })
        lines.push({ x, y: y + p.random(500, p.height - 100) })
      }
      p.stroke(255)
      p.beginShape(p.LINES)
      for (let i = 0; i <= lines.length - 1; i++) {
        p.vertex(lines[i].x, lines[i].y)
      }
      p.endShape()
    }
  }

  // eslint-disable-next-line no-new,new-cap
  new p5(sketch, 'container')
}
</script>

<style>
#container {
  flex: 1;
  min-height: 80vh;
}
</style>
