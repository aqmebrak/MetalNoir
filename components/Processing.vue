<template>
  <div id="container"></div>
</template>

<script>
export default {
  layout: 'default'
}
if (process.client) {
  const p5 = require('p5')
  const frames = 60

  const sketch = function(p) {
    // vars
    let myFont = null
    let brightUp = true

    // consts
    const lines = []
    const colorBrightness = []
    const moonCoord = {
      x: window.innerWidth / 2,
      y: window.innerHeight / 2 - 200
    }

    // init
    for (let i = 0; i < frames; i++) {
      colorBrightness[i] = i * (255 / frames)
    }

    // preload
    p.preload = function() {
      myFont = p.loadFont('./brutal-tooth.otf')
    }

    // setup
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

    // draw
    p.draw = function() {
      p.background(0)
      p.noStroke()
      p.circle(moonCoord.x, moonCoord.y, 150)
      p.stroke(215, 215, 215)
      p.text('NOIRE', window.innerWidth / 2, 100)
      p.textAlign(p.CENTER, p.TOP)

      p.strokeWeight(3)
      const color = brightUp ? colorBrightness.shift() : colorBrightness.pop()

      brightUp ? colorBrightness.push(color) : colorBrightness.unshift(color)
      p.stroke(color)
      if (p.frameCount % frames === 0) {
        brightUp = !brightUp
      }

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
