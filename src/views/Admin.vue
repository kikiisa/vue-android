<template>
  <Navbar />
  <div class="container py-2">
    <div class="row justify-content-center">
      <div class="col-12 text-start">
        <button @click="logout" class="btn btn-dark">
          <i class="fas fa-arrow-left"></i> Logout
        </button>
        <button @click="this.$router.push('form')" class="btn btn-dark ms-1">
          <i class="fas fa-add"></i> Tambah Pengumuman
        </button>
      </div>
      <div class="col-12 col-md-12 mt-2">
        <ul class="list-group">
          <li class="list-group-item d-flex justify-content-between align-items-center" v-for="parse in dataPengumuman" :key="parse.id_pengumuman">
            {{ parse.judul_pengumuman }}
            <div class="row g-1">
              <div class="col-md-6 col-6">
                <router-link :to="`/form-edit/${parse.id_pengumuman}`" class="btn btn-warning">
                  <i class="fas fa-edit"></i>
                </router-link>
              </div>
              <div class="col-md-6 col-6">
                <button @click="deletePost(parse.id_pengumuman)" class="btn btn-danger">
                  <i class="fas fa-trash"></i>
                </button>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
import { useRouter, useRoute } from 'vue-router'
import http from '../url'
import { ref,onMounted } from 'vue'
export default {
  name: "Home",
  components: {
    Navbar,
  },
  setup()
  {
    const router = useRouter()
    const route = useRoute()
    const dataPengumuman = ref([])
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
    const deletePost = async (id) =>
    {
        await http.get(`rest.php?delete=${id}`).then((r)=>{
            FetchPengumuman()
        }).catch((e) => {
            console.log(e)
        })
    }
    const verify = () => 
    {
        if(!localStorage.getItem("status"))
        {
            router.push('/')
        }
    }
    const logout = () =>
    {
        localStorage.removeItem("status")
        router.push('/')
    }
    onMounted(() => {
      verify()
      FetchPengumuman()
    })
    return{
        dataPengumuman,deletePost,logout,verify
    }
  }
};
</script>
<style scoped>
.container {
  margin-top: 10px;
}
</style>
