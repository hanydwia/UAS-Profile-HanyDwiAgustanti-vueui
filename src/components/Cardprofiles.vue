<template>
  <div class="row">
    <div class="col-lg-4 mt-3" v-for="(profile, index) in profiles" :key="index">
      <div class="card">
        <div class="card-body">{{ profile.nama }}</div>
        <div class="card-body">
          <p class="card-text">{{ profile.tgl }}</p>
          <p class="card-text">{{ profile.jenis }}</p>
          <p class="card-text">{{ profile.alamat }}</p>
          <p class="card-text">{{ profile.no_tlp }}</p>
          <p class="card-text">{{ profile.email }}</p>
        </div>
       
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["profiles"],
};
</script>

<style>
</style>