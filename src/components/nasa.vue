<template>
  <div class="container mt-5">
    <div class="container mb-5 mt-5">
      <h1 class="bo mb-3 mt-5">The Best Image Of The Day</h1>
      <img src="../assets/rocket1.png" height="250px" />
      <div>
        <input type="date" class="datee" v-model="keyword" />
        <button class="button" v-b-toggle.collapse @click="searchData()">
          Search
        </button>
      </div>
    </div>
    <div class="mt-5">
      <b-collapse id="collapse">
        <b-card
          v-if="result"
          :title="result.title"
          :img-src="result.url"
          img-top
          tag="article"
          style="max-width: 100rem"
          class="mb-5"
        >
          <b-card-text class="h">{{ result.explanation }}</b-card-text>
        </b-card>
      </b-collapse>
    </div>

    <model v-if="error" @close="showModal = false">
      <h1 slot="body" class="bo">
        Date must be between Jun 16, 1995 and Today
      </h1>
      <h3 slot="footer">
        <button class="button-a mt-5" @click="reset()">Click to reset</button>
      </h3>
    </model>
  </div>
</template>

<script>
import model from "./model";
import axios from "axios";
export default {
  components: {
    model,
  },
  data() {
    return {
      result: {},
      keyword: "",
      error: false,
    };
  },
  methods: {
    searchData() {
      var url =
        "https://api.nasa.gov/planetary/apod?api_key=rWSo915pVNWHhs2nvnix2ow3sh3aABlw9mwYwJuv&date=" +
        this.keyword;
      axios
        .get(url)
        .then((response) => {
          this.result = response.data;
        })
        .catch((err) => {
          console.log("E: " + err);
          this.error = true;
        });
    },

    reset() {
      Object.assign(this.$data, this.$options.data());
    },
  },
};
</script>

<style>
.button {
  background-color: rgb(151, 228, 252);
  border: none;
  color: rgb(17, 0, 255);
  padding: 5px 5px 5px 5px;
  text-align: center;
  display: inline-block;
  margin: 10px 5px;
  font-size: 2rem;
  cursor: pointer;
  border-radius: 12px;
  border: 0.5px solid rgb(151, 228, 252);
  width: 10rem;
}

button:hover {
  color: yellow;
  border: 0.5px solid rgba(0, 0, 0, 0.664);
  background-color: rgba(0, 0, 0, 0.664);
}

.button-a {
  background-color: rgb(174, 206, 255);
  border: none;
  padding: 5px 5px 5px 5px;
  text-align: center;
  display: inline-block;
  margin: 10px 10px;
  font-size: 2vw;
  cursor: pointer;
  border-radius: 15px;
  border: 0.5px solid rgb(42, 5, 250);
  width: 15rem;
}
button-a:hover {
  color: yellow;
  border: 0.5px solid rgba(255, 255, 255, 0.664);
  background-color: rgba(3, 3, 3, 0.664);
}
.bo {
  color: white;
  font-size: 50px;
}

.datee {
  border-radius: 8px;
  padding: 12px;
  border: 2px solid #ffffff;
  font-size: 20px;
  width: 30rem;
  background-color: white;
}
.h {
  font-size: 1.25rem;
}
</style>