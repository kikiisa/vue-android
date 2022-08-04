<template>
    <Navbar/>
    <div class="container mb-4">
      <div class="row justify-content-center">
          <div class="col-12 col-md-6">
              <div class="card mt-3">
                  <div class="card-header bg-dark text-light text-start">Edit Pengumuman</div>
                  <div class="card-body text-start">
                      <div class="alert alert-danger" v-if="validation == true">
                          Harap Periksa Kembali Form Anda
                      </div>
                      <div class="alert alert-success" v-if="flashmessage == true">
                          Pengumuman berhasil di updaet
                      </div>
                      <form @submit.prevent="store">
                        <div class="form-group">
                            <label for="">Judul Pengumuman</label>
                            <input type="text" v-model="form.judul" :class="validation == true ? 'mt-1 is-invalid form-control' : 'form-control mt-1'"  placeholder="Judul Pengumuman">
                        </div>
                        <div class="form-group mt-4">
                            <label for="">Tanggal</label>
                            <input type="date" v-model="form.tanggal" :class="validation == true ? 'mt-1 is-invalid form-control' : 'form-control mt-1'">
                        </div>
                        <div class="form-group mt-4">
                            <label for="">Isi Pengumuman</label>    
                            <textarea :class="validation == true ? 'mt-1 is-invalid form-control' : 'form-control mt-1'" v-model="form.content" cols="30" rows="10"></textarea>
                        </div>
                        <button type="submit" class="btn btn-dark mt-3">simpan</button>
                        <router-link to="/admin" class="btn btn-outline-dark mt-3 ms-2">kembali</router-link>
                      </form>
                  </div>
              </div>
          </div>
      </div>
    </div>
</template>
<script>
import Navbar from "@/components/Navbar.vue";
import http from '../url';
import { useRouter, useRoute } from 'vue-router'
import { reactive, ref,onMounted } from 'vue';
export default {
  name: "Form",
  components: {
    Navbar,
  },
  setup()
  {
        const router = useRouter()
        const route = useRoute()
        const validation = ref(false)
        const flashmessage = ref(false)
        const form = reactive({
            id:"",
            judul:"",
            tanggal:"",
            content:"",
        });
        const store = async () => 
        {
            if(form.judul == "" || form.tanggal == "" || form.content == "")
            {
                validation.value = true
            }else{
                validation.value = false
                flashmessage.value = true
                const send = new FormData()
                send.append("update","");
                send.append("id",form.id)
                send.append("judul",form.judul)
                send.append("tanggal",form.tanggal)
                send.append("content",form.content)
                await http.post('rest.php',send).then((r) => {
                    console.log(r.data)
                }).catch((e)=>{
                    console.log(e)
                })
            }
        }
        const verify = () => 
        {
            if(!localStorage.getItem("status"))
            {
                router.push('/')
            }
        }
        onMounted(()=>{

            verify()
            http.get(`rest.php?detail=${route.params.id}`).then((res) => {
                form.id = res.data[0].id_pengumuman
                form.judul = res.data[0].judul_pengumuman
                form.tanggal = res.data[0].tanggal_pengumuman
                form.content = res.data[0].content_pengumuman
            }).catch((err) => {
                console.log(err)
            })
        })
      return {
          form,validation,flashmessage,store,verify
      }
  }
};
</script>
<style scoped>
    .container{
        margin-top:20px;
    }
</style>
