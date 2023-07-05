<template>
  <div>
    <h1 class="ListKategori">
      List Kategori
    </h1>
    <div>
      <router-link class="button button-add btn btn-primary" :to="`/insert-kategori/`">Tambah Kategori</router-link>
    </div>
    <div class="row justify-content-center">
      <div class="col-lg-4 col-md-6" v-for="(data, index) in category" :key="data.id">
        <div class="card mb-3">
          <div class="card-body">
            <h5 class="card-title">{{ data.kode }}</h5>
          </div>
          <ul class="list-group list-group-flush">
            <li class="list-group-item">Kategori: {{ data.kategori }}</li>
          </ul>
          <div class="card-body">
            <router-link class="button-edit btn btn-primary" :to="`/edit-kategori/`+data.id">Edit</router-link>
            <button class="button-delete btn btn-danger" role="button" @click="hapusKategori(data.id)">Delete</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { ref } from 'vue';

export default {
  data() {
    return {
      category: ref([]),
    };
  },
  mounted() {
    this.getKategoriList();
  },
  methods: {
    getKategoriList() {
      axios
          .get('https://mhdrmaulana.my.id/pustakaku/select_kategori.php')
          .then(response => {
            this.category = response.data;
          })
          .catch(error => {
            console.log(error);
          });
    },
    hapusKategori(id) {
      axios
          .delete(`https://mhdrmaulana.my.id/pustakaku/delete_kategori.php?id=${id}`)
          .then(response => {
            console.log(response.data);
            this.getKategoriList();
          })
          .catch(error => {
            console.log(error);
          });
    },
  },
};
</script>

<style scoped>

</style>