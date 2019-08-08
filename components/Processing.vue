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
      p.createCanvas(1000, window.innerHeight * 0.8)
      p.background(255)
      p.noLoop()
      // p.frameRate(10)
    }

    p.draw = function() {
      // const treesAngle = 20
      p.strokeWeight(3)
      const lines = []

      for (let i = 0; i <= 50; i++) {
        const x = p.random(0, 1000)
        const y = p.random(0, window.innerHeight * 0.8)
        console.log(x, y)
        lines.push({ x, y })
        lines.push({ x, y: y + p.random(500, p.height - 100) })
      }
      p.beginShape(p.LINES)
      for (let i = 0; i <= lines.length - 1; i++) {
        p.vertex(lines[i].x, lines[i].y)
      }
      p.endShape()
      // if (p.frameCount % 600) {
      //   p.clear()
      // }
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
