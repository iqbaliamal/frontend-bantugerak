<template>
    <div class="mt-16">
        <div class="container mx-auto max-w-lg grid grid-cols-1 sm:w-full md:w-5/12">

            <form @submit.prevent="register">
                <div class="bg-white rounded-sm p-5">
                    <div class="divide-y divide-black divide-opacity-10 mb-5">
                        <div class="text-xl text-center font-bold mb-3">
                        REGISTER AKUN
                        </div>
                        <div></div>
                    </div>


                    <div class="mb-2 text-sm">
                        <label class="mt-2">Nama Lengkap</label>
                        <input type="text" v-model="user.name"
                            class="mt-2 appearance-none w-full bg-gray-200 border border-gray-200 rounded h-7 shadow-sm placeholder-gray-600 focus:outline-none focus:placeholder-gray-600 focus:bg-white focus-within:text-gray-600 p-5"
                            placeholder="Nama Lengkap">
                    </div>

                    <div class="mb-2 text-sm">
                        <label class="mt-2">Alamat Email</label>
                        <input type="email" v-model="user.email"
                            class="mt-2 appearance-none w-full bg-gray-200 border border-gray-200 rounded h-7 shadow-sm placeholder-gray-600 focus:outline-none focus:placeholder-gray-600 focus:bg-white focus-within:text-gray-600 p-5"
                            placeholder="Alamat Email">
                    </div>

                    <div class="cols-span-1 mb-5 text-sm">
                        <label class="mt-2">Password</label>
                        <input type="password" v-model="user.password"
                            class="mt-2 appearance-none w-full bg-gray-200 border border-gray-200 rounded h-7 shadow-sm placeholder-gray-600 focus:outline-none focus:placeholder-gray-600 focus:bg-white focus-within:text-gray-600 p-5"
                            placeholder="Password">
                    </div>

                    <div class="cols-span-1 mb-5 text-sm">
                        <label class="mt-2">Konfirmasi Password</label>
                        <input type="password" v-model="user.password_confirmation"
                            class="mt-2 appearance-none w-full bg-gray-200 border border-gray-200 rounded h-7 shadow-sm placeholder-gray-600 focus:outline-none focus:placeholder-gray-600 focus:bg-white focus-within:text-gray-600 p-5"
                            placeholder="Konfirmasi Password">
                    </div>

                    <div>
                        <button
                            class="bg-gray-700 py-1 px-3 text-white rounded-md shadow-md font-bold inline-block w-full focus:outline-none focus:bg-gray-900">DAFTAR</button>
                    </div>

                </div>
            </form>

            <div class="text-center mt-5">
                Sudah punya akun ? <router-link :to="{name: 'login'}" class="underline text-blue-600">Masuk Disini
                    !</router-link>
            </div>

        </div>
    </div>
</template>

<script>

    //hook vue
    import { ref, reactive, onMounted } from 'vue'
    
    //hook vuex
    import { useStore } from 'vuex'
    
    //hook vue router
    import { useRouter } from 'vue-router'
    
    //hook Toast
    import { useToast } from "vue-toastification"

    export default {

        setup() {

            //user state
            const user = reactive({
                name: '',
                email: '',
                password: '',
                password_confirmation: ''
            })

            //validation state
            const validation = ref([])

            //store vuex
            const store = useStore()

            //route
            const router = useRouter()

            //same interface as this.$toast
            const toast = useToast()

            //function register, fungsi ini di jalankan ketika form di submit
            function register() {

                //define variable 
                let name     = user.name
                let email    = user.email
                let password = user.password
                let password_confirmation = user.password_confirmation

               //panggil actions "register" dari module "auth"
                store.dispatch('auth/register', {
                    name,
                    email,
                    password,
                    password_confirmation
                })
                .then(() => {

                    //redirect ke dashboard
                    router.push({name: 'dashboard'})

                    toast.success("Register Berhasil!")

                }).catch(error => {
                    //show validaation message
                    validation.value = error

                    //show validation name with toast
                    if(validation.value.name) {
                        toast.error(`${validation.value.name[0]}`)
                    }

                    //show validation email with toast
                    if(validation.value.email) {
                        toast.error(`${validation.value.email[0]}`)
                    }

                    //show validation password with toast
                    if(validation.value.password) {
                        toast.error(`${validation.value.password[0]}`)
                    }
                })
            }

            //check user is loggedIn
            onMounted(() => {
                if(store.getters['auth/isLoggedIn']) {
                router.push({name: 'dashboard'})
                }
            })

            //return a state and function
            return {
                user,           // <-- state user
                validation,     // <-- state validation
                register,       // <-- method register
                toast           // <-- hook toast
            }

        }

    }
</script>

<style>

</style>