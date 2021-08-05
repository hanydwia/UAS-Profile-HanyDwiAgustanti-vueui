<template>
  
      <form class="row g-3" @submit.prevent="update">
        <div class="col-md-6">
          <label for="inputEmail4" class="form-label">Nama</label>
          <input
            type="text"
            class="form-control"
            id="inputEmail4"
            v-model="profile.nama"
          />
          <div class="alert alert-danger" v-if="validation.nama">
            {{ validation.nama[0] }}
          </div>
        </div>
        <div class="col-md-6">
          <label for="inputPassword4" class="form-label">Tanggal Lahir</label>
          <input
            type="text"
            class="form-control"
            id="inputPassword4"
            v-model="profile.tgl"
          />
          <div class="alert alert-danger" v-if="validation.tgl">
            {{ validation.tgl[0] }}
          </div>
        </div>
        <div class="col-6">
          <label for="inputAddress" class="form-label">Jenis Kelamin</label>
          <input
            type="text"
            class="form-control"
            id="inputAddress"
            v-model="profile.jenis"
          />
          <div class="alert alert-danger" v-if="validation.jenis">
            {{ validation.jenis[0] }}
          </div>
        </div>
        <div class="col-6">
          <label for="inputAddress" class="form-label">Alamat</label>
          <input
            type="text"
            class="form-control"
            id="inputAddress"
            placeholder="Masukan alamat"
            v-model="profile.alamat"
          />
          <div class="alert alert-danger" v-if="validation.alamat">
            {{ validation.alamat[0] }}
          </div>
        </div>
        <div class="col-6">
          <label for="inputAddress" class="form-label">No Telepon</label>
          <input
            type="number"
            class="form-control"
            id="inputAddress"
            v-model="profile.no_tlp"
          />
          <div class="alert alert-danger" v-if="validation.no_tlp">
            {{ validation.no_tlp[0] }}
          </div>
        </div>
        <div class="col-6">
          <label for="inputAddress" class="form-label">Email</label>
          <input
            type="text"
            class="form-control"
            id="inputAddress"
            placeholder="Masukan email"
            v-model="profile.email"
          />
          <div class="alert alert-danger" v-if="validation.email">
            {{ validation.email[0] }}
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
    const profile = reactive({
      nama: "",
      tgl: "",
      jenis: "",
      alamat: "",
      no_tlp: "",
      email: "",
     
    });

    let groups = ref([]);
    const validation = ref([]);

    const router = useRouter();

    const route = useRoute();

    onMounted(() => {
      axios
        .get(`http://127.0.0.1:8000/api/profiles/${route.params.id}/edit`)
        .then((response) => {
          console.log(response.data.data.nama);

          profile.nama = response.data.data.nama;
          profile.tgl = response.data.data.tgl;
          profile.jenis = response.data.data.jenis;
          profile.alamat = response.data.data.alamat;
          profile.no_tlp = response.data.data.no_tlp;
          profile.email = response.data.data.email;
         
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
      let nama = profile.nama;
      let tgl = profile.tgl;
      let jenis = profile.jenis;
      let alamat = profile.alamat;
      let no_tlp = profile.no_tlp;
      let email = profile.email;
      

      axios
        .put(`http://127.0.0.1:8000/api/profiles/${route.params.id}`, {
          nama: nama,
          tgl: tgl,
          jenis: jenis,
          alamat: alamat,
          no_tlp: no_tlp,
          email: email,
         
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
      profile,
      validation,
      router,
      update,
      route,
      
    };
  },
};
</script>
