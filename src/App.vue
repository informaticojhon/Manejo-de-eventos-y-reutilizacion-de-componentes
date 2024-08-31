<script>
import Cita from './components/Cita.vue';

export default {
  components: { Cita },
  data() {
    return {
      paciente: '',
      fecha: '',
      hora: '',
      gravedad: '',
      motivo: '',
      citas: []
    };
  },
  computed: {
    todosLosCamposLlenos() {
      return this.paciente && this.fecha && this.hora && this.gravedad && this.motivo;
    }
  },
  methods: {
    agregarCita() {
      this.citas.push({
        paciente: this.paciente,
        fecha: this.fecha,
        hora: this.hora,
        gravedad: this.gravedad,
        motivo: this.motivo
      });
      this.paciente = '';
      this.fecha = '';
      this.hora = '';
      this.gravedad = '';
      this.motivo = '';
    },
    eliminarCita(index) {
      this.citas.splice(index, 1);
    }
  }
};
</script>
<template>
  <div>
    <form @submit.prevent="agregarCita" class="formulario">
      <div class="form-group">
        <label :style="{ color: paciente ? 'black' : 'red' }">Paciente</label>
        <input v-model="paciente" />
      </div>

      <div class="form-group">
        <label :style="{ color: fecha ? 'black' : 'red' }">Fecha</label>
        <input v-model="fecha" type="date" />
      </div>

      <div class="form-group">
        <label :style="{ color: hora ? 'black' : 'red' }">Hora</label>
        <input v-model="hora" type="time" />
      </div>

      <div class="form-group">
        <label :style="{ color: gravedad ? 'black' : 'red' }">Gravedad</label>
        <select v-model="gravedad">
          <option value="">Seleccionar</option>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
      </div>

      <div class="form-group">
        <label :style="{ color: motivo ? 'black' : 'red' }">Motivo</label>
        <input v-model="motivo" />
      </div>

      <button :disabled="!todosLosCamposLlenos" type="submit">Agregar</button>
    </form>

    <p v-if="citas.length === 0">No hay consultas registradas</p>
    <div class="citas-container">
    <div v-for="(cita, index) in citas" :key="index">
      <Cita :cita="cita" @eliminarCita="eliminarCita(index)" />
    </div>
    </div>
  </div>
</template>



<style scoped>
.formulario {
  display: flex;
  gap: 10px;
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 5px;
}
.form-group {
  display: flex;
  flex-direction: column;
  margin-right: 10px;
  align-items: center;
}

button {
  align-self: flex-end;
  margin-top: 10px;
}
.citas-container{
  display: flex;
  flex-direction: row;
  gap: 20px;
  margin-top: 15px;
}
 </style>
