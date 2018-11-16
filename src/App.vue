<template>
  <!-- También se puede usar una etiqueta con autocierre <html-clock /> -->
  <html-clock theme="red-lcd"></html-clock>
</template>

<script>
  /* Formas de indicar las rutas:
    - . (estándar): Apunta a la carpeta actual donde se encuentra este fichero
    - @ (Webpack): Apunta a la carpeta raíz del proyecto. Necesita un alias-resolve en la config de webpack.
    - ~ (Parcel): Apunta a la carpeta raíz del proyecto. No necesita configuración.
  */
  import HTMLClock from './components/HTMLClock';

  export default {
    name: 'App',
    components: {
      'html-clock': HTMLClock
    }
  }
</script>

<style lang="postcss">
  /* CSS Global que afecta a toda la #app */
  :root {
    height: 100vh;
    background: linear-gradient(80deg, #999, #555, #333);
  }
</style>
