<template>
  <!-- Se parece a Lazy Load pero con componentes, default es lo que se muestra al final fallback es lo que se muestra mientras carga-->
  <Suspense>
    <template #default>
      <Home />
    </template>
    <template #fallback>
      <SplashScreen />
    </template>
  </Suspense>
</template>

<script>
import SplashScreen from "@/components/SplashScreen.vue"
import { defineAsyncComponent } from 'vue';

export default {
  components: {
    SplashScreen,
    //se muestra solo mientras carga la pagina
    Home: defineAsyncComponent(() => 
      //usar promesa para retardar la carga de la app
      new Promise((resolve) => {
        setTimeout(() => {
          resolve(import("./components/Home.vue"))
        }, 2500);
      })
    )
  }
}
</script>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}
* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>