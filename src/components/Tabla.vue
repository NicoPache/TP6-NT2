<template >

  <section class="src-components-tabla">
    
    <div class="container">
    <div v-if="items.length" class="table">
      <table class="table  table ">
        <!-- encabezado de la tabla -->
        <tr>
          <th v-for="(col, index) in getCols" :key="index">{{ col }}</th>
        </tr>

        <!-- filas con los datos -->
        <tr v-for="(item, index) in items" :key="index">
          <td v-for="(col, index) in getCols" :key="index">{{ item[col] }}</td>
        </tr>
      </table>
    </div>
    
    <div v-else-if="getNoHayItems" class="alert alert-warning mt-1">
        no hay personas para mostrar
    </div>
 
  </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-tabla',
    props: [],

    beforeCreate(){
    
    },

    beforeMount(){
    this.getUsuarios()
    },
    mounted () {
    this.nohay()

    },
    data () {
      return {
       urlUsuarios : 'https://60a9668c20a64100173071ea.mockapi.io/people',
       items:[],
       noHayItems:false
      }
    },
    methods: {

       async getUsuarios() {
        try {
          let respuesta = await this.axios(this.urlUsuarios)
          this.items = respuesta.data 
        }   
        catch(error) {
          console.log(error)
        }
      },

     /*  getUsuarios() {
        
      this.axios(this.urlUsuarios).
      then(respuesta =>{this.items = respuesta.data
      })
      .catch( error => console.error(error))
       
      }, */

      nohay(){
        setTimeout(() => {
         if (!this.items.length){
            this.noHayItems= true
          }
          }, 300);
      }
   
    },
    computed: {
        getCols() {
        return Object.keys(this.items[0])
      },
       getNoHayItems(){
        return this.noHayItems
      }

    }
}


</script>

<style scoped lang="css">
  .src-components-tabla {
    text-align: center;
  }
 
</style>
