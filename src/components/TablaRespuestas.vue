<template>
  <div class="hello">
    <h1> Tabla respuestas </h1>
    <div>
       <table class="table table-dark">
        <tr>
          <th>Nro Pregunta</th>
          <th>Respuesta</th>
        </tr>
        <tr v-for="resp in respuestas" :key="resp.id">
          <th>{{resp.pregunta}}</th>
          <th>{{resp.respuesta}}</th>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TablaRespuestas',

  props: {
    msg: String
  },
  data () {
      return {
        respuestas: [
          {pregunta: 1,
          respuesta: " b, d "
          },
          {pregunta: 2,
          respuesta: "c"
          },
          {pregunta: 3,
          respuesta: "b, e"
          }

        ]
      }
    }
}
</script>

<style>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
