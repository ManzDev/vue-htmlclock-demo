<template>
  <html-clock theme="red-lcd"></html-clock>
</template>

<script>
  /* Formas de indicar las rutas:
    - . (estándar): Apunta a la carpeta actual donde se encuentra este fichero
    - @ (Webpack): Apunta a la carpeta raíz del src. Necesita un alias-resolve en la config de webpack (default).
    - / (Parcel): Apunta a la carpeta raíz del src. No necesita configuración.
  */
  import HTMLClock from '/components/HTMLClock';

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
    height: 90vh;
    background: linear-gradient(80deg, #999, #555, #333);
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
