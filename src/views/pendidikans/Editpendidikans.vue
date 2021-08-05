<template>
  
      <form class="row g-3" @submit.prevent="update">
        <div class="col-md-6">
          <label for="inputEmail4" class="form-label">Nama Sekolah</label>
          <input
            type="text"
            class="form-control"
            id="inputEmail4"
            v-model="pendidikan.nama"
          />
          <div class="alert alert-danger" v-if="validation.nama">
            {{ validation.nama[0] }}
          </div>
        </div>
        <div class="col-md-6">
          <label for="inputPassword4" class="form-label">Tahun Ajaran</label>
          <input
            type="text"
            class="form-control"
            id="inputPassword4"
            v-model="pendidikan.tahun"
          />
          <div class="alert alert-danger" v-if="validation.tahun">
            {{ validation.tahun[0] }}
          </div>
        </div>
  
        <div class="col-12">
          <button type="submit" class="btn btn-primary">Edit</button>
        </div>
      </form>
   
</template>
<script>
import { onMounted, reactive, ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";
export default {
  setup() {
    const pendidikan = reactive({
      nama: "",
      tahun: "",
      
     
    });

    let groups = ref([]);
    const validation = ref([]);

    const router = useRouter();

    const route = useRoute();

    onMounted(() => {
      axios
        .get(`http://127.0.0.1:8000/api/pendidikans/${route.params.id}/edit`)
        .then((response) => {
          console.log(response.data.data.nama);

          pendidikan.nama = response.data.data.nama;
          pendidikan.tahun = response.data.data.tahun;
          
         
        })
        .catch((error) => {
          console.log(error.response.data);
        });

         axios
        .get("http://127.0.0.1:8000/api/groups")
        .then((response) => {
          groups.value = response.data.data;
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    });

    function update() {
      let nama = pendidikan.nama;
      let tahun = pendidikan.tahun; 

      axios
        .put(`http://127.0.0.1:8000/api/pendidikans/${route.params.id}`, {
          nama: nama,
          tahun: tahun,
         
         
        })
        .then(() => {
          router.push({
            name: "Home",
          });
        })
        .catch((error) => {
          validation.value = error.response.data;
        });
    }
    return {
      pendidikan,
      validation,
      router,
      update,
      route,
      
    };
  },
};
</script>
