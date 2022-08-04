<template>
  <div class="row justify-content-center">
    <div class="col-md-8 col-12">
      <form class="text-center" role="search">
        <input
          class="form-control me-2 w-100"
          type="search"
          placeholder="Search"
          aria-label="Search"
        />
      </form>
    </div>
  </div>
  <div class="row justify-content-center">
    <div class="col-md-4 col-6">
      <div class="card" id="login" @click="this.$router.push('login')">
        <div class="card-body">
          <img src="../assets/admin.png" width="60" alt="" srcset="" />
          <p class="card-text mt-2">Login</p>
        </div>
      </div>
    </div>
    <div class="col-md-4 col-6">
      <div class="card" id="about">
        <div class="card-body">
          <img src="../assets/about.png" width="60" alt="" srcset="" />
          <div class="card-text mt-2">Tentang</div>
        </div>
      </div>
    </div>
  </div>
  <div class="row justify-content-center mb-4">
    <div class="col-md-8 col-12 mb-2" v-for="parse in dataPengumuman" :key="parse.id_pengumuman">
      <div class="card">
        <div class="card-body text-start">
          <h3>{{ parse.judul_pengumuman }}</h3>
          <h6>oleh : Admin | {{ parse.tanggal_pengumuman }}</h6>
          <div class="content">
              {{ parse.content_pengumuman  }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, onMounted } from "vue";
import http from "../url";
export default {
  setup() {
    const dataPengumuman = ref([]);
    const FetchPengumuman = async () => {
      await http
        .get("rest.php?pengumuman")
        .then((r) => {
          dataPengumuman.value = r.data;
        })
        .catch((e) => {
          console.log(e);
        });
    };
    onMounted(() => {
      FetchPengumuman()
    })
    return{
        dataPengumuman
    }
  },
};
</script>
<style scoped>
.row {
  margin-top: 10px;
}
.content {
  text-align: justify;
}

#login {
  cursor: pointer;
}
#about {
  cursor: pointer;
}
</style>
