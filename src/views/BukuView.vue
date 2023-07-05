<template>
  <div class="container">
    <router-link class="button button-add btn btn-primary" :to="`/insert-buku/`">Tambah Buku</router-link>
    <div class="row">
      <div class="col-md-4" v-for="(data, index) in buku" :key="data.id">
        <div class="card mb-3">
          <div class="row g-0">
            <div class="col-md-4">
              <img :src="data.file_cover" alt="File Cover" class="img-fluid" style="width: 150px">
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">{{ data.judul }}</h5>
                <p class="card-text">Pengarang: {{ data.pengarang }}</p>
                <p class="card-text">Penerbit: {{ data.penerbit }}</p>
                <p class="card-text">Tahun: {{ data.tahun }}</p>
                <p class="card-text">Harga: {{ data.harga }}</p>
                <p class="card-text"><small class="text-body-secondary">Diupload tanggal: {{ data.tanggal_input }}</small></p>
                <div class="card-body" >
                  <router-link class="button-edit btn btn-primary" :to="`/edit-buku/`+data.id">Edit</router-link>
                  <button class="button button-delete btn btn-danger" role="button" @click="hapusBuku(data.id)">Delete</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import {ref} from 'vue';

export default {
  data() {
    return {
      buku: ref([]),
    };
  },
  mounted() {
    this.getBukuList();
  },
  methods: {
    getBukuList() {
      axios
          .get('https://mhdrmaulana.my.id/pustakaku/select_buku.php')
          .then(response => {
            this.buku = response.data;
          })
          .catch(error => {
            console.log(error);
          });
    },
    hapusBuku(id) {
      axios
          .delete(`https://mhdrmaulana.my.id/pustakaku/delete_buku.php?id=${id}`)
          .then(response => {
            console.log(response.data);
            this.getBukuList();
          })
          .catch(error => {
            console.log(error);
          });
    },
  }
};
</script>


<style scoped>

</style>