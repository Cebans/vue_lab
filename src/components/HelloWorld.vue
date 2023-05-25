<template>
  <body>
    <h1>Lista de Personas</h1>
    <section class="section">
      <label>Nombre:</label>
      <input v-model="nuevoNombre" type="text">
    </section>
    <br>
    <section class="section">
      <label>Apellido:</label>
      <input v-model="nuevoApellido" type="text">
    </section>
    <br>
    <section class="section">
      <label>Edad:</label>
      <input v-model.number="nuevaEdad" type="number">
    </section>
    <br>
    <section class="section">
      <label>Cedula:</label>
      <input v-model="nuevaCedula" type="text">
    </section>
    <br>
    <button class="btn-agregar" @click="agregarPersona">Agregar Persona</button>
    <ul>
      <li v-for="(persona, index) in personas" :key="index">
        {{ persona.nombre }} {{ persona.apellido }} - Edad: {{ persona.edad }} - Cedula: {{ persona.cedula }}
        <button class="btn-agregar" @click="eliminarPersona(index)">Eliminar</button>
      </li>
    </ul>
    <p>
      Total de personas: {{ personas.length }}
    </p>
    <p>
      Personas mayores de edad: {{ contadorMayoresEdad }}
    </p>
    <p>
      Personas menores de edad: {{ contadorMenoresEdad }}
    </p>
  </body>
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

body{
 background-color: #f2f2f2;
  color: #333333;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
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
  display: inline-block;
  padding: 10px 20px;
  background-color: blue;
  color: #fff;
  font-size: 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-agregar:hover,
.btn-eliminar:hover {
  background-color: #45a049;
}

.section{

  color: blue;
  font-size: 18px;
  font-weight: bold;
  justify-content:left;
}

</style>
