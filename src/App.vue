<template>
  <section id="app">
    <header @change="img = false">
      <h1>Random gif cat</h1>
      <!-- Input texto -->
      <div>
        <label for="text">Texto:</label>
        <input v-model="texto" type="text" name="text" />
      </div>
      <!-- Color texto -->
      <div class="colorTexto">
        <label for="color">Color texto:</label>
        <select v-model="color" name="color">
          <option value disabled selected>Color del texto</option>
          <option value="red">Rojo</option>
          <option value="blue">Azul</option>
          <option value="green">Verde</option>
          <option value="white">Blanco</option>
          <option value="yellow">Amarillo</option>
        </select>
        <div class="color" v-if="color != '' " :style="{backgroundColor: color}"></div>
      </div>
      <!-- Tamaño texto -->
      <div>
        <label for>Tamaño texto:</label>
        <input v-model="tamano" type="number" />
      </div>
      <!-- Filtro -->
      <div>
        <label for="filtro">Filtro</label>
        <select v-model="filtro" name="filtro">
          <option value disabled selected>Elige un filtro</option>
          <option value="none">Ninguno</option>
          <option value="blur">Desenfoque</option>
          <option value="mono">Mono</option>
          <option value="sepia">Sepia</option>
          <option value="negative">Negativo</option>
          <option value="paint">Pintura</option>
          <option value="pixel">Píxel</option>
        </select>
      </div>
      <button @click="validacion">Obtener mi gatito</button>
    </header>
    <hr />
    <!-- gif generado -->
    <div class="resultado" v-if="img">
      <img :src="url" />
    </div>
  </section>
</template>

<script>
export default {
  name: "Gatos",
  data() {
    return {
      texto: "",
      filtro: "",
      color: "",
      tamano: "",
      img: false,
    };
  },
  methods: {
    validacion() {
      if (
        this.texto == "" ||
        this.filtro == "" ||
        this.color == "" ||
        this.tamano == ""
      ) {
        this.img = false;
        alert("Debes completar todos los campos para generar tu gatito");
      } else {
        this.generarGato();
      }
    },
    generarGato() {
      this.img = true;
    },
  },
  computed: {
    url() {
      return `https://cataas.com/cat/gif/says/${this.texto}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}`;
    },
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  box-sizing: border-box;
}
body {
  background-color: #cdd7d6;
  color: #ffffff;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}
header {
  background-color: #2d3142;
  padding: 20px 0;
  div {
    padding: 6px 0;
  }
  button {
    margin: 15px 0;
    padding: 15px;
    cursor: pointer;
  }
}
.colorTexto {
  display: flex;
  justify-content: center;
  align-items: center;
  .color {
    width: 50px;
    height: 16px;
    border: 1px solid black;
  }
}
.resultado {
  padding: 30px 0;
}
</style>
