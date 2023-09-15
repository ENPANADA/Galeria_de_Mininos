<script>
const API_PATH = "https://api.thecatapi.com/v1/images/search?order=RAND&limit=";
const API_KEY =
  "live_ephlXws9yEYAoQGlcBSsliO6hJgUyvgyJGsUpSmVTMkxvLaltDw9OMzOk8HJNbCW";
const options = {
  method: "GET",
  headers: {
    "x-api-key": API_KEY,
  },
};
export default {
  data() {
    return {
      Imgs: [],
      loading: true,
      Limit_Images: 15,
      Content: true,
    };
  },
  methods: {
    async RandomCats() {
      this.loading = true;
      this.Imgs = [];
      this.Content = false;
      await fetch(API_PATH + this.Limit_Images, options)
        .then((response) => response.json())
        .then((data) => (this.Imgs = data))
        .catch((err) => console.error(err));
      this.loading = false;
      if (this.Imgs.length == 0) {
        this.Content = true;
      } else {
        this.Content = false;
      }
    },
  },
  created() {
    this.RandomCats();
  },
};
</script>

<template>
  <div class="main">
    <h1 class="Titulo">🐱 Galeria de Mininos 🐈</h1>
    <section class="Galeria">
      <div class="info" v-if="loading">
        <span class="spinner">↻</span>
      </div>
      <div class="info" v-if="Content">
        <span style="font-size: 2.5em">☹</span>
        <span>Upps... Algo salio mal</span>
        <span style="font-size: 0.5em"
          >Revisa tu conexión a internet e intenta de nuevo.</span
        >
      </div>
      <img
        class="Images"
        v-for="(Gatito, index) in Imgs"
        :key="index"
        v-bind:src="Gatito.url"
        v-bind:alt="Gatito.id"
      />
    </section>
    <div class="carga">
      <input
        type="range"
        class="range"
        min="1"
        max="100"
        step="1"
        v-model="Limit_Images"
      />
      <span class="input-info">{{
        "De " + Limit_Images + " en " + Limit_Images
      }}</span>
    </div>
    <button class="boton" @click="RandomCats">
      <span v-if="loading">Cargando ...</span>
      <span v-else>Cargar mas 🐈</span>
    </button>
  </div>
</template>

<style scoped>
.main {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100vh;
  border: 1.5em solid rgba(0, 0, 0, 0);
}
.Titulo {
  text-align: center;
  color: azure;
  font-size: 40px;
  font-style: italic;
  text-shadow: 8px 8px 6px rgb(0, 0, 0);
  margin: 10px 0;
}
.Galeria {
  display: flex;
  flex-wrap: wrap;
  max-width: 1400px;
  justify-content: space-evenly;
  align-content: flex-start;
  overflow-y: auto;
  height: 70vh;
  margin: 0 auto;
}
.Images {
  max-height: 180px;
  box-shadow: 8px 8px 12px rgb(0, 0, 0);
  border-radius: 15px;
  transition: transform 0.3s ease-in-out;
  margin: 10px;
  background-color: rgba(0, 0, 0, 0.5);
  background-size: cover;
  min-height: 100px;
  min-width: 100px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.Images:hover {
  transform: scale(1.1);
}

.info {
  font-size: 2em;
  font-weight: bold;
  color: rgba(0, 0, 0, 0.4);
  text-shadow: 3px 3px 4px;
  display: flex;
  height: 100%;
  min-width: 100%;
  flex-direction: column;
  align-items: center;
  text-align: center;
  justify-content: center;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.spinner {
  font-size: 3em;
  margin: 0.5em;
  animation: rotar 1s ease infinite;
}
.boton {
  display: flex;
  color: #fff;
  font-size: 15px;
  font-weight: bold;
  padding: 15px 20px;
  border-radius: 15px;
  background-color: rgba(0, 0, 0, 0.5);
  border: none;
  margin: 10px auto;
  transition: transform 0.3s ease-in-out;
  cursor: pointer;
  box-shadow: 4px 4px 5px rgb(0, 0, 0);
  justify-content: center;
}
.boton:hover {
  transform: scale(1.1);
}

::-webkit-scrollbar {
  width: 8px;
  transition: width 1s ease-in-out;
}
::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.4);
  border-radius: 10px;
}
::-webkit-scrollbar-thumb {
  background: #000;
  border-radius: 10px;
}
::-webkit-scrollbar-thumb:hover {
  background: rgba(0, 0, 0, 0.7);
}
.carga {
  display: flex;
  justify-content: center;
  align-items: center;
}
.range {
  -webkit-appearance: none;
  margin: 15px;
  width: 40%;
  max-width: 300px;
  background-color: rgba(0, 0, 0, 0);
}
.range::-webkit-slider-runnable-track {
  height: 7px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 5px;
}
.range::-webkit-slider-thumb {
  height: 15px;
  width: 15px;
  border-radius: 25px;
  background: rgb(0, 0, 0);
  box-shadow: 4px 4px 5px rgb(0, 0, 0);
  cursor: grab;
  -webkit-appearance: none;
  margin-top: -4px;
  transition: transform 0.2s ease-in-out;
}
.range:hover::-webkit-slider-runnable-track {
  background: rgba(255, 255, 255, 0.6);
}
.range:hover::-webkit-slider-thumb {
  transform: scale(1.5);
}
.range:active::-webkit-slider-thumb {
  cursor: grabbing;
}

.input-info {
  background-color: rgba(0, 0, 0, 0.5);
  padding: 5px 15px;
  color: #fff;
  border-radius: 15px;
  font-size: 13px;
}

@keyframes rotar {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}

@media (max-width: 600px) {
  .main {
    border: 30px solid rgba(0, 0, 0, 0);
  }
  .Titulo {
    font-size: 25px;
  }
  .Galeria {
    gap: 5px;
  }
  .Images {
    max-height: 150px;
    max-width: 200px;
  }
  .boton {
    width: 100%;
  }
  .boton:hover {
    transform: scale(1);
  }
}
</style>
