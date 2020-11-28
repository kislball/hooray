<!-- eslint-disable -->
<template>
  <span v-for="confe in confetti" :style="{ 'top': `${confe.y}%`, 'left': `${confe.x}%`, 'transform': 'scale(' + confe.r + ')' }">{{ confe.character }}</span>
</template>

<style>
* {
  overflow: hidden;
}

span {
  position: absolute;
  font-size: 100px;
}
</style>

<script>

export default {
  data: () => ({
    confetti: []
  }),
  mounted() {
    const characters = ['🥳', '🎉', '✨'];
    this.confetti = new Array(100).fill().map((_, i) => ({
      character: characters[i % characters.length],
      x: Math.random() * 100,
      y: 20 - Math.random() * 100,
      r: 0.1 + Math.random() * 1
    })).sort((a,b) => a.r - b.r);

    function loop() {
      requestAnimationFrame(loop.bind(this));
      this.confetti = this.confetti.map(emoji => {
        emoji.y += 0.7 * emoji.r;
        if (emoji.y > 120) {
          emoji.y = -20;
          emoji.x = Math.random() * 100
        }
        return emoji;
      });
    }
    loop.bind(this)();
  }
};
</script>