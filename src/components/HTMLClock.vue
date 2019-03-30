<template>
  <!-- Recuerda: Sólo un elemento raíz padre -->
  <!-- Usa el prop theme como clase para dar estilo -->
  <div class="html-clock" :class="theme">
    <img class="vue" src="/assets/logo.png" alt="VueJS Logo">
    <div class="lcd">
      <div class="hours">{{ hours | toHuman }}</div>
      <div class="sep">:</div>
      <div class="minutes">{{ minutes | toHuman }}</div>
      <div class="sep">:</div>
      <div class="seconds">{{ seconds | toHuman }}</div>
      <div class="mode">{{ mode }}</div>
    </div>
  </div>
</template>

<script>
  // Constantes que sólo se necesitan dentro del componente
  const THEMES = ['red-lcd', 'green-lcd', 'blue-lcd'];

  export default {
    // Le damos un nombre (útil a la hora de depurar en Vue Dev Tools)
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
        this.hours = date.getHours();
        this.minutes = date.getMinutes();
        this.seconds = date.getSeconds();
        this.mode = this.hours >= 12 ? 'PM' : 'AM';
      },
      // Inicializa el temporizador del reloj
      startTimer() {
        this.tickId = setInterval(this.update, 1000);
      },
      // Detiene el temporizador del reloj
      stopTimer() {
        clearInterval(this.tickId);
      }
    },
    filters: {
      toHuman: v => v.toString().padStart(2, '0')
    },
    // Se ejecuta cuando se monta un componente (similar al constructor)
    mounted() {
      document.title = 'VueClock.js';
      this.startTimer();
    }
  }
</script>

<style lang="postcss" scoped>
  @font-face {
    font-family: 'Digital Numbers';
    src: url("https://raw.githubusercontent.com/s-a/digital-numbers-font/gh-pages/dist/DigitalNumbers-Regular.woff") format("woff");
  }

  /* Contenedor padre */
  .html-clock {
    background: #000;
    border-radius: 15px;
    width: 600px;
    height: 175px;
    margin: 2em auto;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 40px;
    color: var(--textColor);
  }

  /* Cristal LCD del reloj */
  .lcd {
    display: flex;
    align-items: center;
    background: linear-gradient(165deg, transparent 40%, rgba(255, 255, 255, 0.1), transparent 60%), #111;
    padding: 20px;
    font-family: 'Digital Numbers', sans-serif;
    font-size: 72px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  }

  /* Logo de VUE */
  .vue {
    width: 125px;
    transform: scale(1.75);
    user-select: none;
    pointer-events: none;
  }

  .hours,
  .minutes,
  .seconds,
  .sep {
    letter-spacing: -10px;
  }

  /* AM / PM */
  .mode {
    font-size: 22px;
    padding-left: 10px;
  }

  /* Parpadeo de los dos separadores */
  .sep {
    animation: blink 1s linear infinite;
  }

  @keyframes blink {
    0%,
    49% { opacity: 1; }

    50%,
    100% { opacity: 0; }
  }

  /* Themes disponibles */
  .red-lcd {
    --textColor: red;
  }

  .green-lcd {
    --textColor: green;
  }

  .blue-lcd {
    --textColor: blue;
  }
</style>
