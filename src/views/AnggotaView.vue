<template>
  <div>
    <h1 class="ListAnggota">
      List Anggota
    </h1>
    <div>
      <router-link class="button button-add" :to="`/insert-anggota/`">Tambah Anggota</router-link>
    </div>
    <div class="row justify-content-center">
      <div class="col-lg-4 col-md-6" >
        <div class="card mb-3">
          <div class="card-body" v-for="(data, index) in anggota" :key="data.id">
            <h5 class="card-title">{{ data.nama }}</h5>
            <p class="card-text">no.{{ data.nomor }}</p>
            <ul>
              <li class="list-group-item">{{ data.jenis_kelamin }}</li>
              <li class="list-group-item">No. Telepon: {{ data.no_hp }}</li>
              <li class="list-group-item">Alamat: {{ data.alamat }}</li>
              <li class="list-group-item">Tanggal Terdaftar: {{ data.tanggal_terdaftar }}</li>
            </ul>
            <div class="card-body">
              <router-link class="button-edit" :to="`/edit-anggota/`+data.id">Edit</router-link>
              <button class="button-delete" role="button" @click="hapusAnggota(data.id)">Delete</button>
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
      anggota: []
    };
  },
  mounted() {
    this.getAnggotaList();
  },
  methods: {
    getAnggotaList() {
      axios
          .get(`https://mhdrmaulana.my.id/pustakaku/select_anggota.php/`)
          .then(response => {
            this.anggota = response.data;
          })
          .catch(error => {
            console.log(error);
          });
    },
    hapusAnggota(id) {
      axios
          .delete(`https://mhdrmaulana.my.id/pustakaku/delete_anggota.php?id=${id}`)
          .then(response => {
            console.log(response.data);
            this.getAnggotaList();
          })
          .catch(error => {
            console.log(error);
          });
    }
  }
};
</script>

<style>

</style>