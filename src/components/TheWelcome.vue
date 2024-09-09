<script setup>


  const props= defineProps({
    datos:{
      type: Object,
      required: true
    }
  })

  defineEmits(['obtiene-ciudad'])
</script>

<template>
 <div>
    <v-card class="mx-3 bg-blue-grey-lighten-5 text-center py-3">
      <v-img
      class="mt-3"
        :width="300"
        aspect-ratio="16/9"
        cover
        :src="props.datos.img"
      >
      </v-img>
      <v-card-title> Viaje a {{ props.datos.nombre }} </v-card-title>

      <!-- <p>{{ props.hola.impulsora }}</p> -->
      <div>
        <v-btn 
        block
        color="light-blue-darken-4" @click="$emit('preciona-boton', props.datos.id)"
          >Revisa Ruta
        </v-btn>
      </div>
    </v-card>
  </div>

</template>
