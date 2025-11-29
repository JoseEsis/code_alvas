<script setup lang="ts">
import { ref, onMounted } from "vue";

const props = defineProps({
  lead: {
    type: Object,
    required: true,
    default: () => ({}),
  },
});

const emit = defineEmits(["close", "save"]);

// Inicializamos el formulario vacío
const form = ref({
  propiedad: "Vista Hermosa",
  nombre: "",
  celular: "",
  fecha: "",
  tipo: "",
});

// Al montar el componente, copiamos los datos de la tabla al formulario
onMounted(() => {
  if (props.lead) {
    form.value.nombre = props.lead.nombre || "";
    form.value.celular = props.lead.celular || "";
    form.value.tipo = props.lead.tipo || "";
    // Si tienes propiedad en tu objeto lead, úsala: form.value.propiedad = props.lead.propiedad;

    // Tratamiento de Fecha:
    // Si tu fecha viene como "23 / 11 / 25" (DD / MM / YY) hay que convertirla para el input date (YYYY-MM-DD)
    // Este es un ejemplo simple, ajusta según cómo guardes tus fechas realmente.
    // form.value.fecha = '2025-11-23';
    // Por ahora pasamos el valor directo si ya es compatible, o lo dejamos vacío para que el usuario elija.
    form.value.fecha = props.lead.fecha || "";
  }
});

const guardar = () => {
  // Emitimos los datos limpios al padre
  emit("save", { ...form.value });
};
</script>

<template>
  <div class="fixed inset-0 z-50 flex items-center justify-center p-4">
    <div
      class="fixed inset-0 bg-black/50 backdrop-blur-md transition duration-200"
      @click="$emit('close')"
    ></div>

    <div
      class="bg-white w-full max-w-lg rounded-[30px] shadow-2xl z-50 relative p-8 m-auto max-h-[95vh] overflow-y-auto"
    >
      <div class="mb-6">
        <h2 class="text-2xl font-bold text-black mb-1">Editar Lead</h2>
        <p class="text-gray-400 text-sm">Edite la información del lead</p>
      </div>

      <div class="space-y-5">
        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2"
            >Seleccione una propiedad</label
          >
          <div class="relative">
            <select
              v-model="form.propiedad"
              class="w-full appearance-none bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:ring-2 focus:ring-gray-300 outline-none"
            >
              <option>Vista Hermosa</option>
              <option>Lomas del Sur</option>
              <option>Residencial El Prado</option>
            </select>
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-4 text-gray-600"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="2"
                stroke="currentColor"
                class="w-4 h-4"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="m19.5 8.25-7.5 7.5-7.5-7.5"
                />
              </svg>
            </div>
          </div>
        </div>

        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2">Nombre Completo</label>
          <input
            type="text"
            v-model="form.nombre"
            class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:ring-2 focus:ring-gray-300 outline-none"
          />
        </div>

        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2">Celular</label>
          <input
            type="text"
            v-model="form.celular"
            class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:ring-2 focus:ring-gray-300 outline-none"
          />
        </div>

        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2">Fecha</label>
          <div class="relative">
            <input
              type="date"
              v-model="form.fecha"
              class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:ring-2 focus:ring-gray-300 outline-none appearance-none"
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
        </div>

        <div>
          <label class="block text-sm font-semibold text-gray-800 mb-2">Tipo</label>
          <input
            type="text"
            v-model="form.tipo"
            class="w-full bg-gray-200 border-none rounded-xl py-3 px-4 text-gray-800 font-medium focus:ring-2 focus:ring-gray-300 outline-none"
          />
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
              d="M2.25 18.75a60.07 60.07 0 0 1 15.797 2.101c.727.198 1.453-.342 1.453-1.096V18.75M3.75 4.5v.75A.75.75 0 0 1 3 4.5ZM3 18.75v-.75A.75.75 0 0 1 3.75 18.75H3ZM3.75 12h.008v.008H3.75V12Zm.375 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm6.375 0h.008v.008H10.5V12Zm.375 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm6.375 0h.008v.008H17.25V12Zm.375 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Z"
            />
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M20.25 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"
            />
          </svg>
          Guardar Cambios
        </button>
      </div>
    </div>
  </div>
</template>
