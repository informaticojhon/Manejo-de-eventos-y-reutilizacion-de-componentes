<template>
  <div :style="{ backgroundColor: colorGravedad }" class="cita-card">
    <p><strong>Paciente:</strong> {{ cita.paciente }}</p>
    <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
    <p><strong>Hora:</strong> {{ cita.hora }}</p>
    <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
    <button @click="$emit('eliminarCita')">Eliminar</button>
  </div>
</template>

<script>
export default {
  props: ['cita'],
  computed: {
    colorGravedad() {
      switch (this.cita.gravedad) {
        case 'Baja': return 'green';
        case 'Media': return 'yellow';
        case 'Alta': return 'red';
        default: return 'white';
      }
    }
  }
};
</script>

<style scoped>
.cita-card {
  padding: 40px;
  border-radius: 15px;
}
</style>