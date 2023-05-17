<template>
  <div>
    <h1>Lista de Personas</h1>
    <div>
      <label>Nombre:</label>
      <input v-model="nuevoNombre" type="text">
    </div>
    <div>
      <label>Apellido:</label>
      <input v-model="nuevoApellido" type="text">
    </div>
    <div>
      <label>Edad:</label>
      <input v-model.number="nuevaEdad" type="number">
    </div>
    <div>
      <label>Cedula:</label>
      <input v-model="nuevaCedula" type="text">
    </div>
    <button @click="agregarPersona">Agregar Persona</button>
    <ul>
      <li v-for="(persona, index) in personas" :key="index">
        {{ persona.nombre }} {{ persona.apellido }} - Edad: {{ persona.edad }} - Cedula: {{ persona.cedula }}
        <button @click="eliminarPersona(index)">Eliminar</button>
      </li>
    </ul>
    <div>
      Total de personas: {{ personas.length }}
    </div>
    <div>
      Personas mayores de edad: {{ contadorMayoresEdad }}
    </div>
    <div>
      Personas menores de edad: {{ contadorMenoresEdad }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      personas: [],
      nuevoNombre: "",
      nuevoApellido: "",
      nuevaEdad: null,
      nuevaCedula: "",
      contadorMayoresEdad: 0,
      contadorMenoresEdad: 0,
    };
  },
  methods: {
    agregarPersona() {
      const nuevaPersona = {
        nombre: this.nuevoNombre,
        apellido: this.nuevoApellido,
        edad: this.nuevaEdad,
        cedula: this.nuevaCedula,
      };

      this.personas.push(nuevaPersona);

      if (nuevaPersona.edad >= 18) {
        this.contadorMayoresEdad++;
      } else {
        this.contadorMenoresEdad++;
      }

      this.resetForm();
    },
    eliminarPersona(index) {
      const personaEliminada = this.personas[index];

      if (personaEliminada.edad >= 18) {
        this.contadorMayoresEdad--;
      } else {
        this.contadorMenoresEdad--;
      }

      this.personas.splice(index, 1);
    },
    resetForm() {
      this.nuevoNombre = "";
      this.nuevoApellido = "";
      this.nuevaEdad = null;
      this.nuevaCedula = "";
    },
  },
};
</script>

<style scoped>
h1 {
  color: blue;
}

.form-group {
  margin-bottom: 10px;
}

.personas-table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

.personas-table th,
.personas-table td {
  padding: 8px;
  border: 50px solid #ddd;
}

.personas-table th {
  background-color: black;
}

.btn-agregar,
.btn-eliminar {
  padding: 8px 16px;
  border: 50px;
  background-color: #4caf50;
  color: #fff;
  cursor: pointer;
}

.btn-agregar:hover,
.btn-eliminar:hover {
  background-color: #45a049;
}

</style>
