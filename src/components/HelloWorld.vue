<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1 v-if="author.name == 'Oscar'">Eso es correcto</h1>
    <h1 v-else>Esta mal el author</h1>
    <span>{{ author.books.length == 3 ? 'Si' : 'No'}}</span>
    <br>
    <br>
    <!--<li v-for="(value, key) in listaPeces" :key="key"> {{ value }}</li>-->

    <button class="btn btn-success" @click="obtenerDiferentesPhotos()"> Ver Api </button>
    <br>
    <br>
      
  <table class="table table-dark ">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Titulo</th>
      <th scope="col">Url</th>
      <th scope="col">Acciones</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="photos in listaPhotos" :key="photos.id">
      <td>{{ photos.id }}</td>
      <td>{{ photos.title }}</td>
      <td>{{ photos.url }}</td>
      <td> 
        <b-button :to="'/detalle/' + photos.id" class="btn btn-primary"> Ver mas </b-button>
      </td>
    </tr>
  </tbody>
</table>


  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    id: Number,
  },
  data(){
    return {
      author: {
        name: 'Jhon Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      },
      carros: {
        name: null,
        colores: []
      },
      listaPhotos: [],
    }
  },

  created(){
    this.obtenerDiferentesPhotos();
  },

  methods:{
    obtenerDiferentesPhotos(){
      let apiURL = 'https://jsonplaceholder.typicode.com/photos';
      this.listaPhotos= [];

      this.$http.get(apiURL).then(response => {
        if(response.status == 200){
        let data = response.data;

        data.forEach((element, index) =>{
          if (index + 1  <= 20){
            this.listaPhotos.push(element)
          }
        });
        }
      })
      .catch(e => console.log(e))
      .finally(()=>console.log("Siempre me ejecuto al final"))
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
.hello{
  background-color: #42b983;
}
</style>
