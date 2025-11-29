<script setup lang="ts">
import { ref, computed } from "vue";

const props = defineProps({
  lead: {
    type: Object,
    required: false,
    default: () => ({}),
  },
});

const emit = defineEmits(["close"]);

// Datos simulados de visitas disponibles para este lead (o propiedades asociadas)
// En un caso real, esto vendría de tu backend o store
const listaVisitas = [
  {
    nombrePropiedad: "Vista Hermosa",
    tipoInmueble: "Terreno",
    direccion: "Centro, AV. Principal",
    fecha: "21/11/25",
    hora: "9:00 AM",
  },
  {
    nombrePropiedad: "Lomas del Sur",
    tipoInmueble: "Casa",
    direccion: "Zona Sur, Calle 10",
    fecha: "22/11/25",
    hora: "3:00 PM",
  },
];

// Variable reactiva para la selección del dropdown
const visitaSeleccionadaNombre = ref(listaVisitas[0].nombrePropiedad);

// Computada para obtener los datos de la visita seleccionada
const datosVisita = computed(() => {
  return (
    listaVisitas.find((v) => v.nombrePropiedad === visitaSeleccionadaNombre.value) ||
    listaVisitas[0]
  );
});
</script>

<template>
  <div class="fixed inset-0 z-50 flex items-center justify-center p-4">
    <div
      class="fixed inset-0 bg-black/50 backdrop-blur-md transition duration-200"
      @click="$emit('close')"
    ></div>

    <div class="bg-white w-full max-w-4xl rounded-[30px] shadow-2xl z-50 relative p-8 m-auto">
      <button
        @click="$emit('close')"
        class="absolute top-6 right-6 text-black hover:text-gray-600 transition-colors"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="2"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>

      <h2 class="text-2xl font-bold text-black mb-1">Programación de Vista</h2>
      <p class="text-gray-400 text-sm mb-6">Seleccione una propiedad</p>

      <div class="mb-8">
        <div class="relative max-w-sm">
          <select
            v-model="visitaSeleccionadaNombre"
            class="w-full appearance-none bg-gray-200 border-none rounded-xl py-3 px-4 pr-10 text-gray-800 font-medium focus:outline-none focus:ring-2 focus:ring-gray-300 cursor-pointer shadow-inner"
          >
            <option
              v-for="visita in listaVisitas"
              :key="visita.nombrePropiedad"
              :value="visita.nombrePropiedad"
            >
              {{ visita.nombrePropiedad }}
            </option>
          </select>
          <div
            class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-4 text-gray-800"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="2.5"
              stroke="currentColor"
              class="w-4 h-4"
            >
              <path stroke-linecap="round" stroke-linejoin="round" d="m19.5 8.25-7.5 7.5-7.5-7.5" />
            </svg>
          </div>
        </div>
      </div>

      <div class="rounded-[20px] overflow-hidden shadow-md border border-gray-200">
        <div
          class="grid grid-cols-2 px-8 py-4 text-sm font-bold text-gray-400 border-b border-gray-200 bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)]"
        >
          <span class="ml-1">Tipo de Inmueble</span>
          <span class="text-left ml-1">Dirección</span>
        </div>

        <div
          class="grid grid-cols-2 px-8 py-4 text-base font-semibold text-black border-b border-gray-200 bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)]"
        >
          <span>{{ datosVisita.tipoInmueble }}</span>
          <span>{{ datosVisita.direccion }}</span>
        </div>

        <div
          class="grid grid-cols-2 px-8 py-4 text-sm font-bold text-gray-400 border-b border-gray-200 bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)]"
        >
          <span class="ml-1">Fecha de Visita</span>
          <span class="text-left ml-1">Hora de Visita</span>
        </div>

        <div
          class="grid grid-cols-2 px-8 py-4 text-base font-semibold text-black bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)] pb-6"
        >
          <span>{{ datosVisita.fecha }}</span>
          <span>{{ datosVisita.hora }}</span>
        </div>
      </div>
    </div>
  </div>
</template>
