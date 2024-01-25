<template>
  <div>
    <h1 class="header"></h1>
    <div class="container">
      <div class="nav">
        <img class="logo" :src="imagem" alt="" />
        <div class="menu">
          <button class="btn" @click="navigate('home')">{{ nav[0] }}</button>
          <button class="btn" @click="alterarEstiloComponente">
            {{ nav[1] }}
          </button>
          <button class="btn" @click="openContato">{{ nav[2] }}</button>
        </div>
        <contato :open="open" />
        <div class="search">
          <input type="text" class="input" placeholder="Pesquisar" />
        </div>
      </div>
      <div class="content" style="display: flex">
        <img :src="imagem" alt="" style="width: 50%" />
        <img :src="imagem" alt="" style="width: 50%" />
      </div>
    </div>
    <div
      id="carouselExampleSlidesOnly"
      class="carousel slide"
      data-ride="carousel"
    >
      <div class="carousel-inner">
        <div class="carousel-item active">
          <img src="img/logo(2).jpg" alt="..." class="d-block w-100" />
        </div>
        <div class="carousel-item">
          <img :src="imagem" alt="..." class="d-block w-100" />
        </div>
        <div class="carousel-item">
          <img src="img/logo(2).jpg" alt="..." class="d-block w-100" />
        </div>
      </div>

      <!-- Botões de Navegação -->
      <div class="nav-buttons">
        <button class="nav-button" @click="prevSlide">Anterior</button>
        <button class="nav-button" @click="nextSlide">Próximo</button>
      </div>
    </div>
  </div>
</template>

<script>
import TecnologiasSection from "../body/top.vue";
import Contato from "./contato.vue";
import { ref } from "vue";

export default {
  data() {
    return {
      nav: ["Home", "Sobre", "Contato"],
      open: ref(false),
      imagem: "/img/moveis.jpg",
      currentIndex: 0,
    };
  },
  components: {
    Contato,
    TecnologiasSection,
  },
  methods: {
    openContato() {
      this.open = !this.open;
    },

    alterarEstiloComponente() {
      // Emita um evento para notificar o componente alvo sobre a mudança
      this.$emit("alterar-estilo-componente");
    },

    showSlide(index) {
      const carouselInner = document.querySelector(".carousel-inner");
      const slides = document.querySelectorAll(".carousel-item");

      if (index < 0) {
        this.currentIndex = slides.length - 1;
      } else if (index >= slides.length) {
        this.currentIndex = 0;
      } else {
        this.currentIndex = index;
      }

      const translateValue = -this.currentIndex * 100 + "%";
      carouselInner.style.transform = "translateX(" + translateValue + ")";
    },

    prevSlide() {
      this.showSlide(this.currentIndex - 1);
    },

    nextSlide() {
      this.showSlide(this.currentIndex + 1);
    },
  },
};
</script>

<style scoped>
.logo {
  margin-right: 10px;
  margin-left: 110px;
  width: 3%;
  height: 3%;
  border-radius: 50%;
}

.nav-buttons {
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: center;
  display: flex;
  gap: 50px;
  background-color: #333;
}

.carousel {
  overflow: hidden;
  width: 100%;
  max-width: 600px; /* Defina o tamanho desejado do carrossel */
  margin: 20px auto;
}

.carousel-inner {
  width: 100%;
  height: 100%;
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-item {
  min-width: 100%;
  box-sizing: border-box;
}

img {
  width: 100%;
  height: auto;
}

/* Botões de Navegação */
.nav-button {
  cursor: pointer;
  padding: 10px;
  background-color: #333;
  color: #fff;
  border: none;
  outline: none;
}

.nav-button:hover {
  background-color: #555;
}
</style>
