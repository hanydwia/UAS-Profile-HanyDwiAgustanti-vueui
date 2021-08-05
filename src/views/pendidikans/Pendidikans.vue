<template>
  <div class="home">
    <Slider />

    <table class="table">
      <thead>
        <tr>
          <th scope="col">Nama Sekolah</th>
          <th scope="col">Tahun Ajaran</th>
          <th scope="col">Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(pendidikan, index) in pendidikans" :key="index">
          <td>{{ pendidikan.nama}}</td>
          <td>{{ pendidikan.tahun}}</td>
          
          <td>
            <router-link class="btn btn-success" :to="{name:'Editpendidikans', params:{id:pendidikan.id}} "
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
    let pendidikans = ref([])

    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/pendidikans')
      .then(response => {
        pendidikans.value = response.data.data
      })
      .catch(error => {
        console.log(error)
      })
    })



    return {
      pendidikans,
      
    }
  }
};
</script>
