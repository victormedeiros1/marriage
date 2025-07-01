<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const dias = ref(0);
const horas = ref(0);
const minutos = ref(0);
const segundos = ref(0);

const dataDeCasamento = new Date("2032-04-03T00:00:00");

let intervalo;

const atualizarContador = () => {
  const agora = new Date();
  const diferenca = dataDeCasamento - agora;

  if (diferenca <= 0) {
    dias.value = 0;
    horas.value = 0;
    minutos.value = 0;
    segundos.value = 0;
    clearInterval(intervalo);
    return;
  }

  dias.value = Math.floor(diferenca / (1000 * 60 * 60 * 24));
  horas.value = Math.floor((diferenca / (1000 * 60 * 60)) % 24);
  minutos.value = Math.floor((diferenca / (1000 * 60)) % 60);
  segundos.value = Math.floor((diferenca / 1000) % 60);
};

onMounted(() => {
  atualizarContador();
  intervalo = setInterval(atualizarContador, 1000);
});

onUnmounted(() => {
  clearInterval(intervalo);
});
</script>

<template>
  <div class="container">
    <div class="casamento">
      <div class="fotos">
        <div class="coracao">
          <img class="foto foto-a" width="100%" src="./assets/duda.png" />
          <img class="foto foto-b" width="100%" src="./assets/vikin.png" />
        </div>
      </div>
      <h1 class="titulo">Faltam</h1>
      <h2 class="contador-regressivo">
        {{ dias }} dias {{ horas }} horas {{ minutos }} minutos
        {{ segundos }} segundos
      </h2>
      <h3 class="subtitulo">PARA O NOSSO CASAMENTO</h3>
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 100%;
  min-height: 100dvh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;

  background: linear-gradient(270deg, #8e2de2, #f953c6, #8e2de2);
  background-size: 600% 600%;
  animation: gradientMove 10s ease infinite;
}

@keyframes gradientMove {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.casamento {
  width: 600px;
}

h1,
h2,
h3 {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

h1 {
  font-size: 4rem;
  margin-bottom: 1rem;
}

h2 {
  margin-bottom: 2rem;
}

h3 {
  font-size: 2rem;
  font-weight: bold;
}

.foto {
  width: 100px;
  filter: drop-shadow(0 0 10px rgba(0, 0, 0, 0.5));
}

.fotos {
  width: 100%;
  height: 200px;
}

.coracao {
  animation: float 3s ease-in-out infinite;
}

@keyframes float {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>
