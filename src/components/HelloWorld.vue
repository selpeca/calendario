<template>
  <Qalendar 
    :events="eventos"
    :config="config"
  />
</template>

<script setup>
import {  ref, onMounted  } from 'vue'
import { Qalendar } from "qalendar";
const personas = [
  {
    name:"Sebastian",
    color: "green",
  },
  {
    name:"Fabio",
    color: "blue",
  },
  {
    name:"Cristian",
    color: "red",
  },
  {
    name:"Sergio",
    color: "yellow",
  },
  {
    name:"Ray",
    color: "pink",
  },
]
const eventos = ref([]);
const config = {
  locale: "es-ES",
  defaultMode: "month"
}
const generarTurnos = () => {
    const turnos = [];
    let fecha = new Date(2024, 8, 1);
    let contador = 0;
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
            title: personas[contador].name,
            time: { start: fechaFormateada, end:fechaFormateada },
            color: personas[contador].color,
            id: get_uuidv4(),
          }
        );
        
      fecha.setDate(fecha.getDate() + 1);
      if (contador === personas.length - 1) {
        contador = 0;
      }else{
        contador++;
      }
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