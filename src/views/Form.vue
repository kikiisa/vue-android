<template>
  <Navbar />
  <div class="container mb-4">
    <div class="row justify-content-center">
      <div class="col-12 col-md-6">
        <div class="card">
          <div class="card-header bg-dark text-light text-start">
            Tambah Pengumuman
          </div>
          <div class="card-body text-start">
            <div class="alert alert-danger" v-if="validation == true">
              Harap Periksa Kembali Form Anda
            </div>
            <div class="alert alert-success" v-if="flashmessage == true">
              Pengumuman berhasil di tambahkan
            </div>
            <form @submit.prevent="store">
              <div class="form-group">
                <label for="">Judul Pengumuman</label>
                <input
                  type="text"
                  v-model="form.judul"
                  :class="
                    validation == true
                      ? 'mt-1 is-invalid form-control'
                      : 'form-control mt-1'
                  "
                  placeholder="Judul Pengumuman"
                />
              </div>
              <div class="form-group mt-4">
                <label for="">Tanggal</label>
                <input
                  type="date"
                  v-model="form.tanggal"
                  :class="
                    validation == true
                      ? 'mt-1 is-invalid form-control'
                      : 'form-control mt-1'
                  "
                />
              </div>
              <div class="form-group mt-4">
                <label for="">Isi Pengumuman</label>
                <textarea
                  :class="
                    validation == true
                      ? 'mt-1 is-invalid form-control'
                      : 'form-control mt-1'
                  "
                  v-model="form.content"
                  cols="30"
                  rows="10"
                ></textarea>
              </div>
              <button type="submit" class="btn btn-dark mt-3">simpan</button>
              <router-link to="/admin" class="btn btn-outline-dark mt-3 ms-2"
                >kembali</router-link
              >
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
import http from "../url";
import { useRouter, useRoute } from "vue-router";
import { onMounted, reactive, ref, router } from "vue";
export default {
  name: "Form",
  components: {
    Navbar,
  },
  setup() {
    const router = useRouter();
    const route = useRoute();
    const validation = ref(false);
    const flashmessage = ref(false);
    const form = reactive({
      judul: "",
      tanggal: "",
      content: "",
    });
    onMounted(()=>{
        verify()
    })
    const verify = () => 
    {
        if(!localStorage.getItem("status"))
        {
            router.push('/')
        }
    }
    const store = () => {
      if (form.judul == "" || form.tanggal == "" || form.content == "") {
        validation.value = true;
      } else {
        const send = new FormData();
        send.append("tambah", "");
        send.append("judul", form.judul);
        send.append("tanggal", form.tanggal);
        send.append("content", form.content);
        send.append("id_admin", 1);
        http
          .post("rest.php", send)
          .then((r) => {
            if (r.data.status == true) {
              validation.value = false;
              flashmessage.value = true;
              form.judul = "";
              form.tanggal = "";
              form.content = "";
              setTimeout(() => {
                this.$router.push({ path: "/admin" });
              }, 1500);
            }
          })
          .catch((e) => {
            console.log(e);
          });
      }
    };
    return {
      form,
      store,
      validation,
      flashmessage,
      verify
    };
  },
};
</script>
<style scoped>
.container {
  margin-top: 40px;
}
</style>
