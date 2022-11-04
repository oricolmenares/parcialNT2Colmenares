<template>
  <section class="src-componentes-formulario-av">
    <div class="jumbotron">
      <h2> Formulario</h2>
      <hr>
      <hr>
      <br>

      <vue-form :state="formState" @submit.prevent="enviar()">
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            type="text" 
            id="nombre" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.nombre" 
            name="nombre"
            required
            :minlength="nombreMinLength"
            no-espacios
          >
          <!-- mensajes de validación -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no permite espacios intermedios
            </div>

          </field-messages>
        </validate>
    
        <br>
        <validate tag="div">
          <label for="dni">Descripcion</label>
          <input 
            type="text" 
            id="descripcion" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.descripcion" 
            name="dni"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          </field-messages>
        </validate>

        <br>
        <validate tag="div">
          <label for="pago">Importe</label>
          <input 
            type="number" 
            id="pago" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.pago" 
            name="pago"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="pago" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          </field-messages>
        </validate>
        <br>

        <button class="btn btn-success my-3" :disabled="formState.$invalid">Enviar</button>

      </vue-form>    
      <hr>
      <table v-if="datosForm.length" class = "table">
        <tr>
          <th>Nombre</th>
          <th>Descripcion</th>
          <th>Importe</th>
          <th>Fecha</th>
        </tr>
        <tr v-for="dato in datosForm" :key="dato.dni">
          <th> {{ dato.nombre }} </th>
          <th> {{ dato.descripcion }} </th>
          <th> $ {{ dato.pago }} </th>
          <th> {{ dato.fecha }} </th>
        </tr>
        <tr :class="{ green: calcularTotal()<1000, 
          violet: calcularTotal()>1000 }"> 
          <p>Total: {{ calcularTotal() }} </p>
        </tr>
    </table>

      <hr>
 

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-formulario-av',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState : {},
        formData: this.getInitialData(),
        nombreMinLength: 3,
        datosForm:[]
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre: null,
          descripcion: null,
          pago: null,
          fecha: null,
          esMenor: false,
          esMayor: false,
          total: null
        }
      },
      
      enviar() {
        let datoGasto = {...this.formData}
        datoGasto.fecha = new Date().toLocaleString()

        this.datosForm.push(datoGasto)
        this.formData = this.getInitialData()
        this.formState._reset()
      },

      calcularTotal() {
        let totalSum = this.datosForm.reduce(function (acc, obj) { return acc + Number(obj.pago); }, 0);

        //console.log(totalSum)

        return totalSum
      

      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-formulario-av {

  }

  .jumbotron {
    color: darkblue;
  }

  hr {
    background-color: #bbb;
  }

  .violet {
    background: magenta;
  }

  .naranja {
    background: orange;
  }

  .green {
    background-color: green;
  }

  pre {
    color: white;
  }
</style>
