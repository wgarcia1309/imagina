<template>
  <div class="card is-one-quarter">
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-128x128">
            <img :src="imagen.url" class="bordes" alt="Placeholder image">
          </figure>
        </div>
        <div class="media-content">
          <h3>{{ propuesta.title }}</h3>
        </div>
      </div>

      <div class="content wave position">
        <User class="margin-top" :usuario="userjson"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import env from '../config/env.js'
import User from '../components/User.vue'
export default {
  name: 'TarjetaPropuesta',
  data (){
    return {      
      userjson:Object
      }
  },
  components :{
    User
  },
    props: {
    propuesta: Object,
    imagen: Object
  },
created(){
    axios.get(`${env.endpoint}/users/${this.propuesta.userId}`).then((response) => {
        this.userjson = response.data
      })
}
}
</script>

<style scope>
.card-content{
  padding: 1rem;
}
.card{
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
  transition: all 0.3s cubic-bezier(.25,.8,.25,1);
}
.card:hover {
  box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
}
.margin-top{
  margin-top: 20px;
}
.is-one-quarter{
  width: 31%;
  margin: 10px;
}
.bordes{
  border-radius:30px;
}
</style>
