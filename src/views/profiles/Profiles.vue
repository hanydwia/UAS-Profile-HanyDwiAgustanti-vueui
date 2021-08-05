<template>
  <div class="home">
    <Slider />

    <table class="table">
      <thead>
        <tr>
          <th scope="col">Nama</th>
          <th scope="col">Tanggal Lahir</th>
          <th scope="col">Jenis Kelamin</th>
          <th scope="col">Alamat</th>
          <th scope="col">No Telepon</th>
          <th scope="col">Email</th>
          <th scope="col">Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(profile, index) in profiles" :key="index">
          <td>{{ profile.nama}}</td>
          <td>{{ profile.tgl}}</td>
          <td>{{ profile.jenis}}</td>
          <td>{{ profile.alamat}}</td>
          <td>{{ profile.no_tlp}}</td>
          <td>{{ profile.email}}</td>
          <td>
            <router-link class="btn btn-success" :to="{name:'Editprofiles', params:{id:profile.id}} "
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
    let profiles = ref([])

    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/profiles')
      .then(response => {
        profiles.value = response.data.data
      })
      .catch(error => {
        console.log(error)
      })
    })



    return {
      profiles,
      
    }
  }
};
</script>
