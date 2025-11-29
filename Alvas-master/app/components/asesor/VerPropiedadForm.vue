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

// 1. DEFINIR LOS DATOS DE LAS PROPIEDADES
const listaPropiedades = [
  {
    nombre: "Vista Hermosa",
    tipo: "Terreno",
    ubicacion: "Zona Norte, Sector A",
    tamano: "112 m2",
    monto: "$ 4.000",
    partida: "P-12345-2025 o Tomo 123, Folio 456",
    servicios: "Agua, Luz, Drenaje",
    habitaciones: "N/A", // Es terreno
  },
  {
    nombre: "Lomas del Sur",
    tipo: "Casa",
    ubicacion: "Zona Sur, Av. Principal",
    tamano: "250 m2",
    monto: "$ 85.000",
    partida: "P-98765-2024 o Tomo 555, Folio 12",
    servicios: "Todos los servicios",
    habitaciones: "4",
  },
  {
    nombre: "Residencial El Prado",
    tipo: "Departamento",
    ubicacion: "Centro Histórico",
    tamano: "90 m2",
    monto: "$ 60.000",
    partida: "P-55555-2023 o Tomo 88, Folio 99",
    servicios: "Agua, Luz, Gas, Internet",
    habitaciones: "2",
  },
];

// Variable reactiva para la selección
const propiedadSeleccionada = ref(listaPropiedades[0].nombre);

// 2. COMPUTADA PARA OBTENER LOS DATOS DE LA SELECCIÓN ACTUAL
const datosActuales = computed(() => {
  return (
    listaPropiedades.find((p) => p.nombre === propiedadSeleccionada.value) || listaPropiedades[0]
  );
});
</script>

<template>
  <div class="fixed inset-0 z-50 flex items-center justify-center">
    <div
      class="fixed inset-0 bg-black/50 backdrop-blur-md transition duration-200"
      @click="$emit('close')"
    ></div>

    <div
      class="bg-white w-full max-w-5xl rounded-[30px] shadow-2xl z-50 relative p-8 m-4 max-h-[90vh] overflow-y-auto"
    >
      <button
        @click="$emit('close')"
        class="absolute top-6 right-6 text-gray-500 hover:text-black transition-colors"
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

      <div class="mb-8">
        <label class="block text-gray-400 text-sm mb-2 font-medium">Seleccione una propiedad</label>
        <div class="relative max-w-sm">
          <select
            v-model="propiedadSeleccionada"
            class="w-full appearance-none bg-gray-200 border border-gray-300 text-gray-800 py-2 px-4 pr-8 rounded-lg shadow-inner focus:outline-none focus:ring-2 focus:ring-gray-400 font-medium"
          >
            <option v-for="prop in listaPropiedades" :key="prop.nombre" :value="prop.nombre">
              {{ prop.nombre }}
            </option>
          </select>
          <div
            class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
          >
            <svg
              class="fill-current h-4 w-4"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
            >
              <path
                d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
              />
            </svg>
          </div>
        </div>
      </div>

      <div class="mb-8">
        <div class="rounded-[20px] overflow-hidden shadow-md border border-gray-200">
          <div class="bg-black text-white px-6 py-4 font-semibold text-lg">
            Información de Propiedad
          </div>

          <div
            class="grid grid-cols-5 px-6 py-4 text-sm font-bold text-gray-800 border-b border-gray-300 bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)]"
          >
            <span>Tipo de Propiedad</span>
            <span class="text-center">Ubicación</span>
            <span class="text-center">Tamaño</span>
            <span class="text-center">Monto</span>
            <span class="text-right">Partida Registral</span>
          </div>

          <div
            class="grid grid-cols-5 px-6 py-6 text-sm text-gray-800 font-medium items-center bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)]"
          >
            <span>{{ datosActuales.tipo }}</span>
            <span class="text-center">{{ datosActuales.ubicacion }}</span>
            <span class="text-center">{{ datosActuales.tamano }}</span>
            <span class="text-center font-bold">{{ datosActuales.monto }}</span>
            <span class="text-right">{{ datosActuales.partida }}</span>
          </div>
        </div>
      </div>

      <h3 class="text-lg font-semibold text-gray-800 mb-4 ml-1">Detalles del Inmueble</h3>

      <div class="mb-4">
        <div class="rounded-[20px] overflow-hidden shadow-md border border-gray-200">
          <div class="bg-black text-white px-6 py-4 font-semibold text-lg">
            Detalles del Inmueble
          </div>

          <div
            class="grid grid-cols-3 px-6 py-4 text-sm font-bold text-gray-800 border-b border-gray-300 bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)]"
          >
            <span>Propiedad</span>
            <span class="text-center">Servicios</span>
            <span class="text-center">Habitaciones</span>
          </div>

          <div
            class="grid grid-cols-3 px-6 py-6 text-sm text-gray-800 font-medium items-center bg-[linear-gradient(180deg,#F9F9F9_10%,#EAEAEA_64%)]"
          >
            <span>{{ datosActuales.tipo }}</span>
            <span class="text-center">{{ datosActuales.servicios }}</span>
            <span class="text-center">{{ datosActuales.habitaciones }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
