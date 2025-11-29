<script setup lang="ts">
import { ref, onMounted } from "vue";

// Props: Recibimos el lead al que se le programará la visita (opcional)
const props = defineProps({
  lead: {
    type: Object,
    required: false,
    default: () => ({ nombre: "", celular: "" }),
  },
});

const emit = defineEmits(["close", "save"]);

// Estado del formulario
const form = ref({
  propiedad: "Vista Hermosa", // Valor por defecto o el que venga del lead
  fecha: "",
  hora: "",
});

// Al montar, si ya hay datos previos, los cargamos (opcional)
onMounted(() => {
  // Aquí podrías pre-llenar datos si estuvieras editando
});

const guardar = () => {
  // Validar si es necesario antes de emitir
  if (!form.value.fecha || !form.value.hora) {
    alert("Por favor seleccione fecha y hora");
    return;
  }

  // Emitimos el objeto con los datos de la nueva visita
  // Incluimos datos del lead para mostrar en la tabla Citas
  emit("save", {
    ...form.value,
    nombreCliente: props.lead.nombre || "Cliente Nuevo",
    celularCliente: props.lead.celular || "Sin número",
  });

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
      <h2 class="text-2xl font-bold text-black mb-6">Programar Visita</h2>

      <div class="space-y-5">
        <div>
          <div
            class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium"
          >
            {{ form.propiedad }}
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
            <p class="text-xs text-gray-400 mt-1 ml-1">Seleccione la fecha de la visita</p>
          </div>
        </div>

        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2">Hora de la Visita</label>
          <div class="relative">
            <input
              type="time"
              v-model="form.hora"
              class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:outline-none focus:ring-2 focus:ring-gray-300 appearance-none"
            />
            <p class="text-xs text-gray-400 mt-1 ml-1">Hora local en formato de 24 horas</p>
          </div>
        </div>
      </div>

      <div class="flex items-center justify-between gap-4 mt-8">
        <button
          @click="$emit('close')"
          class="flex-1 py-3 border border-black text-black rounded-[15px] font-semibold hover:bg-gray-50 transition-colors"
        >
          Cancelar
        </button>

        <button
          @click="guardar"
          class="flex-1 py-3 bg-black text-white rounded-[15px] font-semibold hover:bg-gray-800 transition-colors"
        >
          Programar Visita
        </button>
      </div>
    </div>
  </div>
</template>
