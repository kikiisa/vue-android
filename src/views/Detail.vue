<template>
    <Navbar/>
    <div class="container">
      <div class="row justify-content-center">
          <div class="col-12 col-md-6">
              <div class="card">
                  <div class="card-header bg-dark text-light text-start">Edit Pengumuman</div>
                  <div class="card-body text-start">
                      <form action="" method="post">
                        <div class="form-group">
                            <label for="">Judul Pengumuman</label>
                            <input type="text" class="form-control mt-1" placeholder="Judul Pengumuman">
                        </div>
                        <div class="form-group mt-4">
                            <label for="">Tanggal</label>
                            <input type="date" class="form-control mt-1">
                        </div>
                        <div class="form-group mt-4">
                            <label for="">Isi Pengumuman</label>
                        
                        </div>
                      </form>
                  </div>
              </div>
          </div>
      </div>
    </div>
</template>
<script>
import { reactive } from 'vue'
import Navbar from "@/components/Navbar.vue";
export default {
  name: "Home",
  components: {
    Navbar
  },
  setup()
  {
  }
};
</script>
<style scoped>
    .container{
        margin-top:40px;
    }
</style>
