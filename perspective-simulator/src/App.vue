<template>
  <h2>CSS3 Perspective Simulator</h2>
    <main>
      <section class="settings">
        <div class="settings-container">
          <label>perspective: {{perspective}}px;</label>
          <input v-model="perspective" type="range" min="0" max="999" />

          <label>rotateX: {{rotateX}}deg; </label>
          <input v-model="rotateX" type="range" min="-180" max="180" />

          <label>rotateY: {{rotateY}}deg; </label>
          <input v-model="rotateY" type="range" min="-180" max="180" />

          <label>rotateZ: {{rotateZ}}deg; </label>
          <input v-model="rotateZ" type="range" min="-180" max="180" />

          <div class="showStyle" :class="isCopy ? 'copied' : 'notCopied'">{{ box }}</div>

          <div class="actionBtn">
            <button class="reset" type="button" @click="reset">Reset</button>
            <button class="copy" type="button" @click="copyStyles">Copy</button>
          </div>
        </div>
      </section>
      <section class="output">
        <div class="box-container">
          <div class="box" :style="box"></div>
        </div>
      </section>
    </main>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      perspective: 100,
      rotateX: 0,
      rotateY: 0,
      rotateZ: 0,
      isCopy: false
    }
  },
  methods: {
    reset() {
      this.perspective = 100;
      this.rotateX = 0;
      this.rotateY = 0;
      this.rotateZ = 0;
    },
    copyStyles() {
      this.isCopy = true;
      const style = `transform: ${this.box.transform};`;
      navigator.clipboard.writeText(style).then(() => {
        setTimeout(() => { 
          this.isCopy = false;
      }, 3000)
      }).catch((error) => {
        console.error('Failed to copy styles: ', error);
      });
    }
  },
  computed: {
    box() {
      return {
        transform: `perspective(${this.perspective}px) rotateX(${this.rotateX}deg) rotateY(${this.rotateY}deg) rotateZ(${this.rotateZ}deg)`
      }
    }
  }
}
</script>

<style src="./assets/style.css" />
