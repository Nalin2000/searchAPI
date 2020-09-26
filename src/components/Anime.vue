<template>
  <div class="contsiner">
    <!--กรอก-->
    <input type="text" v-model="keyword" />
    <button class="button" @click="searchData()">Search</button>
    <!--{{result}} อยู่ใน tag ไม่ต้องใช้ปีกกาแต่ต้อง : or bind-->
    <!--check ว่าค่าเจอไหม-->
    <b-card
      v-for="data in result"
      :key="data.mal_id"
      :title="data.title"
      :img-src="data.image_url"
      :img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem"
      class="mb-2"
    >
      <b-card-text>{{ data.synopsis }}</b-card-text>
      <b-button :href="data.url" variant="primary">Go somewhere</b-button>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      result: null,
      keyword: "",
      err: false,
    };
  },
  methods: {
    searchData() {
      axios
        .get(
          "https://api.jikan.moe/v3/search/anime?q=" + this.keyword + "&page=1"
        )
        .then((response) => {
          this.result = response.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
.button {
  background-color: rgb(151, 228, 252);
  border: none;
  padding: 5px 5px 5px 5px;
  text-align: center;
  display: inline-block;
  margin: 10px 5px;
  font-size: 2vw;
  cursor: pointer;
  border-radius: 50px;
  border: 0.5px solid rgb(151, 228, 252);
  width: 30vw;
}
button:hover {
  color: rgb(255, 0, 0);
  border: 0.5px solid rgba(245, 126, 146, 0.267);
  background-color: rgba(245, 126, 146, 0.267);
}
</style>