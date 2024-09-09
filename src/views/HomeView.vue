<script setup>
import { reactive } from 'vue';
import TheWelcome from '@/components/TheWelcome.vue';

import CircleProgress from "vue3-circle-progress-bar";
import "vue3-circle-progress/dist/circle-progress.css";


const muestraDatos=reactive({
      id:null,
      nombre: "",
      distancia: 0 ,
      costo: 0,
      tiempo: 0,
      seguro: "",
      img:"",
      ruta:[]
})
const bd = 
  [
    {
      id:1,
      nombre: "Universidad",
      distancia: 25 ,
      costo: 5,
      tiempo: 58,
      seguro: 10,
      img:"https://metro.cdmx.gob.mx/storage/app/media/La%20red/linea3/universidad.png",
      ruta:["Villa de Aragón", "Dirección Buenavista-Bajar en Guerrero", "Transbordar a linea 3 dirección Universidad-Bajar en Universidad"]
    },
    {
      id:2,
      nombre: "Ciudad Azteca",
      distancia: 25 ,
            costo: 5,
            tiempo: 1.00,
            seguro: 50,
            img:"https://mexicocity.cdmx.gob.mx/wp-content/uploads/2020/05/ciudadazteca-300x300.png",
            ruta:
            ["Villa de Aragón", "Dirección Buenavista-Bajar en San Lázaro", "Transbordar a líne 1 dirección Observatorio-Bajar en Pino Suarez", ]
    },
    {
            id:3,
            nombre:"Naucalpan",
            distancia: 20.7 ,
            costos: 5,
            tiempo: 1.04,
            seguro: 100,
            ruta:
            ["Villa de Aragón", "Dirección Buenavista-Guerrero", "Transbordar a líne 3 dirección Universidad-Bajar en Hidalgo, Tranbordar en la linea 2 dire ccion a Cuatro Caminos y bajar en la ultima estación", ]
},  
  ]

  const obtieneCiudad = (id)=>{
      // console.log('Precionando', id)
  const obtieneDireccion = bd.filter((item) => item.id === id)[0]
  console.log('se muestra', obtieneDireccion, id)
  if (obtieneDireccion) {
    console.log(true)
    // muestraDatos.id = obtieneDireccion.id
    // muestraDatos.nombre = obtieneDireccion.nombre
    // muestraDatos.km = obtieneDireccion.km
    // console.log(muestraDatos.id)
    Object.assign(muestraDatos, obtieneDireccion)
    console.log('MuestraDAtos', muestraDatos)
  } else {
    console.log(false)
  }
  }

</script>

<template>
  <div class="w-full bg-indigo-darken-4">
    <v-container id="translate-x-custom" class="translate-y3">
      <v-card class="mx-auto bg-blue-grey-lighten-5">
        <v-card-title class="text-center py-10 "> <h1>Informacion del viaje</h1> </v-card-title>
      </v-card>
    </v-container>
  </div>

  <v-container class="mt-10 d-flex justify-content-center">
    <TheWelcome v-for="datos in bd" :datos="datos" :key="datos.id" @preciona-boton="obtieneCiudad" />
    <!-- <TheWelcome :hola="hola.mensaje.despedida" /> -->
  </v-container>

  <!-- Muestra la informacion -->
  <div v-if="muestraDatos.id" class="mt-10 mx-16">
    <h2 class="text-center mb-3">Viaje a: {{ muestraDatos.nombre }}</h2>
    <v-card class="my-3 bg-blue-grey-lighten-5">
      <v-row>
        <v-col>
      <v-card-text>
        <h3>
          id: <strong>{{ muestraDatos.id }}</strong>
        </h3>
        <h3>
          Distancia: <strong> {{ muestraDatos.distancia }} Km.</strong>
        </h3>
        <h3>Ruta</h3>
        <div v-for="i in muestraDatos.ruta" :key="i.id">
          <li class="font-xl"><strong>{{ i }}</strong></li>
        </div>
      </v-card-text>
    </v-col>
    <v-col>
      <div>
        <h3>
          Costo: <strong>$ {{ muestraDatos.costo }}</strong>
        </h3>
      </div>
      <div>
    <h3>Tiempo: <strong>{{ muestraDatos.tiempo }} {{ muestraDatos.tiempo<10?" Hora":" Minutos"  }}</strong></h3>
  </div>
      <div>
        <h3 id="seguridad" class="px-4"> Seguridad {{ muestraDatos.seguro }} %</h3>
    <CircleProgress
    :percent="muestraDatos.seguro"
    />
  </div>
    </v-col>
    </v-row>
    </v-card>

  </div>
</template>

<style scoped>
#translate-x-custom {
  transform: translateY(3rem);
}

.translate-y-custom {
  transform: translateY(5rem);
}
#seguridad{
  transform: translateY(7rem);
  
}
</style>
