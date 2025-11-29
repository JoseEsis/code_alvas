<script setup lang="ts">
import { ref } from "vue";

const props = defineProps({
  lead: {
    type: Object,
    required: false,
    default: () => ({}),
  },
});

const emit = defineEmits(["close", "guardar"]);

// Variable para el texto de la observación
const observacionTexto = ref("");

const guardarObservacion = () => {
  // Aquí puedes añadir la lógica para guardar
  console.log("Guardando observación:", observacionTexto.value);
  emit("guardar", observacionTexto.value); // Emitir evento al padre si es necesario
  emit("close");
};
</script>

<template>
  <div class="fixed inset-0 z-50 flex items-center justify-center">
    <div
      class="fixed inset-0 bg-black/50 backdrop-blur-md transition duration-200"
      @click="$emit('close')"
    ></div>

    <div class="bg-white w-full max-w-2xl rounded-[20px] shadow-2xl z-50 relative p-8 m-4">
      <div class="mb-6 relative">
        <textarea
          v-model="observacionTexto"
          class="w-full h-48 p-4 border border-gray-300 rounded-[15px] resize-none focus:outline-none focus:ring-2 focus:ring-gray-200 text-gray-700 placeholder-gray-400 text-lg"
          placeholder="Escriba su comentario"
        ></textarea>
      </div>

      <div class="flex justify-end gap-4">
        <button
          @click="$emit('close')"
          class="px-8 py-2 rounded-full border border-gray-400 text-gray-700 font-medium hover:bg-gray-50 transition-colors"
        >
          Cancelar
        </button>

        <button
          @click="guardarObservacion"
          class="px-8 py-2 rounded-full bg-black text-white font-medium hover:bg-gray-800 transition-colors"
        >
          Aceptar
        </button>
      </div>
    </div>
  </div>
</template>
