<template>
  <h2>CSS3 Perspective Playground</h2>
    <main>
      <section class="settings">
        <div class="settings-container">
          <label>perspective: 0px;</label>
          <input type="range" min="0" max="999" />

          <label>rotateX: 0deg; </label>
          <input type="range" min="-180" max="180" />

          <label>rotateY: 0deg; </label>
          <input type="range" min="-180" max="180" />

          <label>rotateZ: 0deg; </label>
          <input type="range" min="-180" max="180" />

          <button type="button">Reset</button>
          <button type="button">Copy</button>
        </div>
      </section>
      <section class="output">
        <div class="box-container">
          <div class="box"></div>
        </div>
      </section>
    </main>
</template>

<script>

export default {
  name: 'App',
  
}
</script>

<style>

</style>
