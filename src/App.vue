<script setup>
import { ref } from 'vue'
import Loading from 'vue-loading-overlay'
import 'vue-loading-overlay/dist/css/index.css'
import Swal from 'sweetalert2'
import toast from '@/utils/toast.js'
import SearchInput from '@/components/SearchInput.vue'

const client_number = ref('')
const show_client = ref(false)
const loading = ref(false)
const show_alert = ref(false)

const client = {
  name: 'Josiel Alonso De Picado'
}

function onSubmit() {
  loading.value = true

  setTimeout(() => {
    show_client.value = true
    loading.value = false
  }, 1000)
}

function markAttendance() {
  Swal.fire({
    title: '¿Marcar asistencia?',
    icon: 'warning',
    showCancelButton: true,
    confirmButtonColor: '#0b3875',
    cancelButtonColor: '#e74a3b',
    confirmButtonText: 'Marcar',
    cancelButtonText: 'Cancelar'
  }).then((result) => {
    if (result.isConfirmed) {
      loading.value = true
      setTimeout(() => {
        show_client.value = false
        loading.value = false
        toast.success('Registrado correctamente!')
      }, 1000)
      showAlert()
    } else {
      show_client.value = false
    }

    client_number.value = ''
  })
}

function showAlert() {
  show_alert.value = true
  setTimeout(() => {
    show_alert.value = false
  }, 3000)
}
</script>

<template>
  <section class="bg-primary text-white w-full">
    <Loading v-model:active="loading" :is-full-page="true" />
    <header class="p-5">
      <img alt="" class="w-14 h-auto" src="/logo-ag.svg" />
    </header>
    <div class="w-full flex items-center justify-center mb-4">
      <form class="text-center p-5 max-w-xl" @submit.prevent="onSubmit">
        <h5 class="text-5xl lg:text-4xl font-bold mb-7">Registro de asistencia</h5>
        <div class="text-sm font-light mb-7 leading-relaxed">
          Consulta el estado de tu plan y registra tu asistencia fácilmente.
        </div>
        <SearchInput v-model="client_number" />
      </form>
    </div>
  </section>
  <section v-if="show_client" class="bg-white text-gray-800 h-full mb-4">
    <div class="w-full flex items-center justify-center flex-col mb-4 gap-2 px-5">
      <span class="font-bold capitalize text-slate-600">
        {{ client.name }}
      </span>
      <span class="text-slate-600 max-w-xl">Pesas (30 dias)</span>
      <span class="text-slate-600 max-w-xl">del 16 de Abril al 15 de Mayo</span>
      <span class="text-danger text-xs"> Expira en 7 dias </span>
      <span class="bg-green-100 text-green-600 rounded-2xl px-6 py-2 mt-3"> Activo </span>
      <button
        class="mt-4 bg-danger text-white w-full rounded-2xl text-center py-4 font-bold text-lg max-w-xl"
        type="button"
        @click.stop="markAttendance"
      >
        Marcar asistencia
      </button>
    </div>
  </section>
  <section v-else class="bg-white text-gray-800 h-full mb-4">
    <div class="w-full flex items-center justify-center flex-col mb-4 gap-2 px-5">
      <Transition mode="out-in" name="slide-up">
        <span
          v-if="show_alert"
          class="text-danger bg-red-100 w-full text-center py-2 rounded-2xl max-w-xl"
        >
          Que tengas un excelente entreno! 💪
        </span>
        <div v-else class="flex flex-col w-full items-center gap-2">
          <span class="font-medium text-lg text-primary">¡Bienvenido de nuevo! </span>
          <span class="text-primary bg-blue-100 w-full text-center py-2 rounded-2xl max-w-xl">
            Aquí podrás ver el estado de tu plan 😊
          </span>
        </div>
      </Transition>
    </div>
  </section>
</template>

<style>
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.25s ease-out;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(30px);
}

.slide-up-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
</style>
