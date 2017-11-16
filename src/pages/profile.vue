<template>
    <!--个人主页-->
    <main-layout>
        <div class="container">

        </div>

    </main-layout>
</template>

<script>
    import MainLayout from '../layouts/Main.vue'
    import '../main.css'
    import '../css/signIn.css'

    export default {
        components: {
            MainLayout
        },
        data() {
            return {
                formData: {
                    username: '',
                    password: ''
                },
                error: {
                    status: true,
                    msg: 'test msg'
                },
                apiUrl:"http://127.0.0.1/user/"
            }
        },
        methods: {
            submit:async function () {
                const data={
                    username:this.formData.username,
                    password:this.formData.password
                }
                const res=await this.$axios.post(`${this.apiUrl}login`,this.formData)

                console.log(res.data)

                if (!res.data.status){
                    //出错
                    this.error =res.data
                }
                else {
                    this.$localStorage.set("username",this.formData.username)
                    console.log(this.$localStorage.get("username"))
                    this.$router.push({path:'/'})
                }
            }
        }
    }



</script>

