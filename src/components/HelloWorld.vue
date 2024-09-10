<template>
  <Qalendar 
    :events="eventos"
    :config="config"
  />
</template>

<script setup>
import {  ref, onMounted  } from 'vue'
import { Qalendar } from "qalendar";
const eventos = ref([{
    title: "SEBASTIAN",
    time: { start: "2024-09-16", end: "2024-09-16" },
    color: "blue",
    isEditable: true,
    id: "753944708f0f",
    description: "SEBASTIAN"
  },
  {
    title: "Ralph on holiday",
    with: "Rachel Greene",
    time: { start: "2022-05-10", end: "2022-05-22" },
    color: "green",
    isEditable: true,
    id: "5602b6f589fc"
  }
]);
const config = {
  locale: "es-ES",
  defaultMode: "month"
}
const generarTurnos = () => {
    const turnos = [];
    let fecha = new Date(2024, 8, 1);
    while (fecha.getMonth() === 8) {
      if (fecha.getDay() === 0) {
        fecha.setDate(fecha.getDate() + 1);
      }
        
        const año = fecha.getFullYear();
        const mes = String(fecha.getMonth() + 1).padStart(2, '0'); // Añadir un 0 delante si es necesario
        const día = String(fecha.getDate()).padStart(2, '0');
        const fechaFormateada = `${año}-${mes}-${día}`;
        turnos.push(
          {
            title: "SEBASTIAN",
            time: { start: fechaFormateada, end:fechaFormateada },
            color: "blue",
            isEditable: true,
            id: get_uuidv4(),
            description: "SEBASTIAN"
          }
        );
        
      const dias_a_sumar = fecha.getDay() > 3 ? 5:4;
      fecha.setDate(fecha.getDate() + dias_a_sumar);
    }

    return turnos;
}
const get_uuidv4 =() =>{
  return "10000000-1000-4000-8000-100000000000".replace(/[018]/g, c =>
    (+c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> +c / 4).toString(16)
  );
}
onMounted(()=>{
  eventos.value = generarTurnos();
})
</script>

<style>
  @import "qalendar/dist/style.css";
</style>