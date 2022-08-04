<template>
    <div class="row justify-content-center">
        <div class="col-md-6 col-11">
            <div class="card text-start">
                <div class="card-body">
                    <div class="alert alert-danger" v-if="message == true">Maaf Username dan Password anda salah</div>
                    <h5>MASUK AKUN</h5>
                    <hr>
                    <form @submit.prevent="checkLogin">
                        <div class="form-group">
                            <label for="email">Alamat Email</label>
                            <input type="text" required v-model="dataUser.email" placeholder="Alamat Email" class="mt-2 form-control">
                        </div>
                        <div class="form-group mt-4">
                            <label for="email">Password</label>
                            <input type="text" required v-model="dataUser.password" placeholder="Password" class="mt-2 form-control">
                        </div>
                        <button type="submit" class="btn btn-dark mt-4 w-100">Masuk</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { ref,reactive } from 'vue'
import { useRouter, useRoute } from 'vue-router'
export default {
    setup() {
        const router = useRouter()
        const route = useRoute()
        const message = ref(false)
        const dataUser = reactive({
            email:"",
            password:""
        });

        const checkLogin = () => 
        {
            if(dataUser.email == "admin@gmail.com" && dataUser.password == "123")
            {
                message.value = false
                localStorage.setItem("status","login");
                router.push('admin')
            }else{
                message.value = true
            }
        }
        return{
            dataUser,checkLogin,message
        }
    },
}
</script>
<style scoped>
   
</style>

