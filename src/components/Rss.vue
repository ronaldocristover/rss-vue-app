<template>
  <div>
    <div class="row">
      <div class="container">
        <div class="form-group">
          <label>Sumber RSS</label>
          <select v-model="rssSource" class="form-control">
            <option value="">Pilih RSS</option>
            <option value="1">Suara.com</option>
            <option value="2">Vice.com</option>
            <option value="3">Tempo RSS</option>
            <option value="4">CNN Indonesia</option>
            <option value="5">CNBC Indonesia</option>
          </select>
        </div>
        <div class="form-group">
          <label>Cari Konten</label>
          <input
            type="text"
            class="form-control"
            v-model="searchKey"
            placeholder="Search"
          />
        </div>
        <button class="btn btn-primary" v-on:click="cari">Cari</button>
      </div>
    </div>
    <div class="row">
      <div class="container">
        <h1>Search Result</h1>
        <!-- Hasil pencarian -->
        <div class="card mt-5" v-for="rss in rssList" :key="rss.link">
            <div class="card-body">
                <h5 class="card-title">{{rss.title}}</h5>
                <p class="card-text" v-html="rss.content"></p>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
const axios = require("axios");

export default {
  data: function () {
    return {
      searchKey: "",
      rssSource: "",
      rssList: "",
    };
  },
  methods: {
    cari: function () {
      console.log(this.rssSource);
      let self = this;

      var config = {
        method: "get",
        url: `http://127.0.0.1:9001/rss?key=${this.searchKey}&source=${this.rssSource}`,
        headers: {},
      };

      axios(config)
        .then(function (res) {
          self.rssList = res.data;
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>