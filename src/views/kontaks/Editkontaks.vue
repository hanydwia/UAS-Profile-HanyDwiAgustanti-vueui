<template>
  
      <form class="row g-3" @submit.prevent="update">
        <div class="col-md-6">
          <label for="inputEmail4" class="form-label">Email</label>
          <input
            type="text"
            class="form-control"
            id="inputEmail4"
            v-model="kontak.email"
          />
          <div class="alert alert-danger" v-if="validation.email">
            {{ validation.email[0] }}
          </div>
        </div>
        <div class="col-md-6">
          <label for="inputPassword4" class="form-label">No Telepon</label>
          <input
            type="text"
            class="form-control"
            id="inputPassword4"
            v-model="kontak.no_tlp"
          />
          <div class="alert alert-danger" v-if="validation.no_tlp">
            {{ validation.no_tlp[0] }}
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
    const kontak = reactive({
      email: "",
      no_tlp: "",
      
     
    });

    let groups = ref([]);
    const validation = ref([]);

    const router = useRouter();

    const route = useRoute();

    onMounted(() => {
      axios
        .get(`http://127.0.0.1:8000/api/kontaks/${route.params.id}/edit`)
        .then((response) => {
          console.log(response.data.data.email);

          kontak.email = response.data.data.email;
          kontak.no_tlp = response.data.data.no_tlp;
          
         
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
      let email = kontak.email;
      let no_tlp = kontak.no_tlp; 

      axios
        .put(`http://127.0.0.1:8000/api/kontaks/${route.params.id}`, {
          email: email,
          no_tlp: no_tlp,
         
         
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
      kontak,
      validation,
      router,
      update,
      route,
      
    };
  },
};
</script>
