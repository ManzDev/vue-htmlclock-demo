<template>
  <!-- Recuerda: Sólo un elemento raíz padre -->
  <!-- Usa el prop theme como clase para dar estilo -->
  <div class="html-clock" :class="theme">
    <div class="lcd">
      <img src="~/assets/logo.png" alt="VueJS Logo">
      <div class="hours">{{ hours }}</div>
      <div class="sep">:</div>
      <div class="minutes">{{ minutes }}</div>
      <div class="sep">:</div>
      <div class="seconds">{{ seconds }}</div>
      <div class="mode">{{ mode }}</div>
    </div>
  </div>
</template>

<script>
  // Constantes que sólo se necesitan dentro del componente
  const THEMES = ['red-lcd', 'green-lcd', 'blue-lcd'];

  export default {
    // Si se omite, es un componente anónimo
    name: 'HTMLClock',
    // Props detallados (con tipado, validación y valores por defecto)
    props: {
      theme: {
        type: String,
        required: false,
        default: 'red-lcd',
        validator: value => THEMES.includes(value)
      }
    },
    // Datos locales del componente (inicializados)
    // RECUERDA: Usar una función (factoría) para devolver objeto data
    data() {
      return {
        hours: '--',
        minutes: '--',
        seconds: '--',
        mode: '--',
      }
    },
    // Funciones del componente
    methods: {
      // Actualiza las horas, minutos y segundos del reloj
      update() {
        const date = new Date();
        this.hours = date.getHours().toString().padStart(2, '0');
        this.minutes = date.getMinutes().toString().padStart(2, '0');
        this.seconds = date.getSeconds().toString().padStart(2, '0');
        this.mode = this.hours >= 12 ? 'PM' : 'AM';
      },
      // Inicializa el timer del reloj
      start() {
        this.tickId = setInterval(this.update, 1000);
      },
      // Para el timer del reloj
      stop() {
        clearInterval(this.tickId);
      }
    },
    // Se ejecuta cuando se monta un componente (similar al constructor)
    mounted() {
      document.title = 'VueClock.js';
      this.start();
    }
  };
</script>

<style lang="postcss" scoped>
  @font-face {
    font-family: 'Digital Numbers';
    src: url("https://raw.githubusercontent.com/s-a/digital-numbers-font/gh-pages/dist/DigitalNumbers-Regular.woff") format("woff");
  }

  /* Contenedor padre */
  .html-clock {
    background: #000;
    width: 600px;
    height: 175px;
    margin: 2em auto;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 40px;
  }

  /* Cristal LCD del reloj */
  .lcd {
    display: flex;
    align-items: center;
    background: linear-gradient(165deg, transparent 40%, rgba(255, 255, 255, 0.1), transparent 60%), #111;
    padding: 20px;
    font-family: 'Digital Numbers', sans-serif;
    font-size: 64px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);

    & img {
      width: 75px;
      transform: scale(2) translateX(-5px);
    }
  }

  /* AM / PM */
  .mode { font-size: 22px; }

  /* Parpadeo de los dos separadores */
  .sep { animation: blink 1s linear infinite; }

  @keyframes blink {
    0%,
    49% { opacity: 1; }

    50%,
    100% { opacity: 0; }
  }

  /* Themes disponibles */
  .red-lcd { color: red; }
  .green-lcd { color: green; }
  .blue-lcd { color: blue; }
</style>
