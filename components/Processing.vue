<template>
  <div id="container"></div>
</template>

<script>
export default {
  layout: 'default'
}
if (process.client) {
  const p5 = require('p5')
  const frames = 5
  const sketch = function(p) {
    let myFont = null
    const lines = []
    const colorBrightness = []
    let brightUp = true

    for (let i = 0; i < frames; i++) {
      colorBrightness[i] = i * (255 / frames)
    }

    console.log(colorBrightness)

    p.preload = function() {
      myFont = p.loadFont('./brutal-tooth.otf')
    }

    p.setup = function() {
      p.createCanvas(window.innerWidth, window.innerHeight)
      p.background(0)
      p.frameRate(frames)
      p.textFont(myFont)
      p.textSize(200)
      for (let i = 0; i <= 10; i++) {
        const x = p.random(0, window.innerWidth)
        const y = p.random(500, window.innerHeight)
        lines.push({ x, y })
        lines.push({ x, y: y + p.random(500, p.height - 100) })
      }
    }

    p.draw = function() {
      p.background(0)
      p.fill(255)
      p.stroke(0)
      p.text('NOIRE', window.innerWidth / 2, 100)
      p.textAlign(p.CENTER, p.TOP)

      p.strokeWeight(3)

      if (p.frameCount % frames === 0) {
        brightUp = !brightUp
      }

      const color = brightUp ? colorBrightness.shift() : colorBrightness.pop()
      console.log(color)

      brightUp ? colorBrightness.push(color) : colorBrightness.unshift(color)
      p.stroke(color)

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
