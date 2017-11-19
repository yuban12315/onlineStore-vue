<template>
    <!--管理员界面-->
    <main-layout>


    </main-layout>
</template>

<script>
    import MainLayout from '../layouts/Main.vue'
    import '../css/main.css'

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
                apiUrl: "http://127.0.0.1/goods/",
                user: {
                    username: '',
                    money: 0
                },
                page: 0,
                chargeMoney: null,
                goodsList: []
            }
        },
        methods: {
            async getUser() {
                const res = await this.$axios.get('http://127.0.0.1/user/getUser')
                if (res.data !== null) {
                    this.user = res.data
                }
            },
            async charge() {
                if (this.chargeMoney < 0) {
                    return
                }
                const user = {
                    username: this.user.username,
                    money: parseInt(this.user.money) + parseInt(this.chargeMoney)
                }
                const res = await this.$axios.post(this.apiUrl + 'charge', this.user)
                if (res.status) {
                    this.user.money = parseInt(this.user.money) + parseInt(this.chargeMoney)
                    this.chargeMoney = null
                }

            },
            async checkAdmin() {
                let res = await this.$axios.get(`http://127.0.0.1/user/logged`)
                const logged = res.data
                if (!logged) {
                    this.$router.go('/')
                }
                res = await this.$axios.get('http://127.0.0.1/user/getUser')
                if (res.data.type==="admin");
                else {
                    this.$router.go('/')
                }
            }
        },
        async created() {
            this.checkAdmin()
        }
    }


</script>
<style scoped>
</style>

