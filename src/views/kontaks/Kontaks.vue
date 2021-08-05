<template>
  <div class="home">
    <Slider />

    <table class="table">
      <thead>
        <tr>
          <th scope="col">Email</th>
          <th scope="col">No Telepon</th>
          <th scope="col">Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(kontak, index) in kontaks" :key="index">
          <td>{{ kontak.email}}</td>
          <td>{{ kontak.no_tlp}}</td>
          
          <td>
            <router-link class="btn btn-success" :to="{name:'Editkontaks', params:{id:kontak.id}} "
              >Edit</router-link
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
import Slider from "@/components/Slider.vue";
import { onMounted, ref } from 'vue';

export default {
  name: "Home",
  components: {
    Slider,
    
  },
  setup(){
    let kontaks = ref([])

    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/kontaks')
      .then(response => {
        kontaks.value = response.data.data
      })
      .catch(error => {
        console.log(error)
      })
    })



    return {
      kontaks,
      
    }
  }
};
</script>
