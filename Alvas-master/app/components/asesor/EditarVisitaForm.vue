<script setup lang="ts">
import { ref, onMounted } from "vue";

const props = defineProps({
  lead: {
    type: Object,
    required: false,
    default: () => ({}),
  },
});

const emit = defineEmits(["close", "save"]);

// Datos del formulario
const form = ref({
  propiedad: "Vista Hermosa",
  fecha: "2025-03-12", // Formato YYYY-MM-DD para que el input date lo lea correctamente
  hora: "23:50", // Formato HH:mm
});

// Lista de propiedades (Terrenos)
const propiedades = ["Vista Hermosa", "Lomas del Sur", "Residencial El Prado"];

onMounted(() => {
  // Aquí podrías cargar los datos reales del lead si vinieran en los props
  if (props.lead) {
    // Ejemplo de asignación si tuvieras estos campos en el objeto lead
    // form.value.propiedad = props.lead.propiedad || 'Vista Hermosa';
  }
});

const guardar = () => {
  console.log("Guardando visita:", form.value);
  emit("save", form.value);
  emit("close");
};
</script>

<template>
  <div class="fixed inset-0 z-50 flex items-center justify-center p-4">
    <div
      class="fixed inset-0 bg-black/50 backdrop-blur-md transition duration-200"
      @click="$emit('close')"
    ></div>

    <div class="bg-white w-full max-w-md rounded-[30px] shadow-2xl z-50 relative p-8 m-auto">
      <div class="mb-6">
        <h2 class="text-2xl font-bold text-black mb-1">Editar Visita</h2>
        <p class="text-gray-400 text-sm">Actualizar la información de la visita</p>
      </div>

      <div class="space-y-5">
        <div>
          <div class="relative">
            <select
              v-model="form.propiedad"
              class="w-full appearance-none bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:outline-none focus:ring-2 focus:ring-gray-300"
            >
              <option v-for="prop in propiedades" :key="prop" :value="prop">
                {{ prop }}
              </option>
            </select>
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-4 text-gray-600"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
                class="w-5 h-5"
              >
                <path
                  fill-rule="evenodd"
                  d="M5.23 7.21a.75.75 0 011.06.02L10 11.168l3.71-3.938a.75.75 0 111.08 1.04l-4.25 4.5a.75.75 0 01-1.08 0l-4.25-4.5a.75.75 0 01.02-1.06z"
                  clip-rule="evenodd"
                />
              </svg>
            </div>
          </div>
        </div>

        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2">Fecha de la Visita</label>
          <div class="relative">
            <input
              type="date"
              v-model="form.fecha"
              class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:outline-none focus:ring-2 focus:ring-gray-300 appearance-none"
            />
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-4 text-gray-600"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-5 h-5"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 0 1 2.25-2.25h13.5A2.25 2.25 0 0 1 21 7.5v11.25m-18 0A2.25 2.25 0 0 0 5.25 21h13.5A2.25 2.25 0 0 0 21 18.75m-18 0v-7.5A2.25 2.25 0 0 1 5.25 9h13.5A2.25 2.25 0 0 1 21 11.25v7.5"
                />
              </svg>
            </div>
          </div>
          <p class="text-xs text-gray-400 mt-1 ml-1">Seleccione la fecha de la visita</p>
        </div>

        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2">Hora de la Visita</label>
          <div class="relative">
            <input
              type="time"
              v-model="form.hora"
              class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:outline-none focus:ring-2 focus:ring-gray-300 appearance-none"
            />
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-4 text-gray-600"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-5 h-5"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M12 6v6h4.5m4.5 0a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"
                />
              </svg>
            </div>
          </div>
          <p class="text-xs text-gray-400 mt-1 ml-1">Hora local en formato de 24 horas</p>
        </div>
      </div>

      <div class="flex items-center justify-between gap-4 mt-8 pt-2">
        <button
          @click="$emit('close')"
          class="flex-1 py-3 border border-black text-black rounded-[15px] font-semibold hover:bg-gray-50 transition-colors"
        >
          Cancelar
        </button>

        <button
          @click="guardar"
          class="flex-1 py-3 bg-black text-white rounded-[15px] font-semibold hover:bg-gray-800 transition-colors flex items-center justify-center gap-2"
        >
          Guardar Cambios
        </button>
      </div>
    </div>
  </div>
</template>
