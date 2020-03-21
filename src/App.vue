<template>
  <div id="app">
    <h1>Vue Animals</h1>
    <h4>By Arvin Poddar</h4>
    <div class="grid">
      <animal v-for="n in 140" :key="n" size="60px" />
    </div>

    <h1>Animals:</h1>
    <h4>Choose from dozens of animals (just a few options below):</h4>
    <div class="grid">
      <div v-for="animal in sampleAnimals" :key="animal">
        <animal :name="animal" color="red" />
        {{ animal }}
      </div>
    </div>

    <h1>Colors:</h1>
    <h4>Use a pre-set color or any CSS hexcode:</h4>
    <div class="grid">
      <div v-for="color in colors" :key="color">
        <animal name="elephant" :color="color" />
        {{ color }}
      </div>
      <div>
        <animal name="elephant" color="#0025D6" />
        #0025D6 (custom)
      </div>
    </div>

    <h1>Sizes:</h1>
    <h4>Use any valid CSS width (max of 200px):</h4>
    <div class="grid">
      <div>
        <animal name="alligator" color="blue" />
        Default (70px)
      </div>
      <div>
        <animal name="alligator" color="blue" size="100px" />
        100px
      </div>
      <div>
        <animal name="alligator" color="blue" size="20vw" />
        20vw
      </div>
    </div>

    <h1>Shapes:</h1>
    <h4>Use circles, rounded, or square avatar shapes</h4>
    <div class="grid">
      <div>
        <animal name="panda" color="green" />
        circle
      </div>
      <div>
        <animal name="panda" color="green" rounded />
        rounded
      </div>
      <div>
        <animal name="panda" color="green" square />
        square
      </div>
    </div>

    <h1>Dancing:</h1>
    <h4>Use the "dance" prop to make them dance!</h4>
    <div class="grid">
      <div v-for="n in 6" :key="n">
        <animal dance />
      </div>
    </div>

    <h1 style="margin-bottom: 50px;">View the README for more info!</h1>
  </div>
</template>

<script>
import animal from "./components/Animal.vue";

export default {
  name: "App",
  components: {
    animal
  },
  data() {
    return {
      colors: [
        "red",
        "orange",
        "yellow",
        "green",
        "blue",
        "purple",
        "teal",
        "none"
      ],
      sampleAnimals: [
        "panda",
        "elephant",
        "kraken",
        "koala",
        "dolphin",
        "alligator"
      ]
    };
  }
};
</script>

<style lang="scss">
body {
  background-color: #1d1d1d;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  width: 100%;
  h1,
  h4 {
    line-height: 100%;
    margin: 10px auto;
  }
  h1 {
    margin-top: 50px;
  }
}

.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.grid > div {
  margin: 5px;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
