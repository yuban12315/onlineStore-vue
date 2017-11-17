<template>
    <main-layout>

        <!--商品详情页-->
        <div class="container">
            <div class="detail row">
                <div class="col-md-6 col-sm-12">
                    <img class="img-fluid" v-bind:src="goods.picture"/>
                </div>
                <div class="col-md-6 col-sm-12 msg row">
                    <div class="col-12 nopadding">
                        <h4 class="title">{{goods.name}}</h4>
                        <div>
                            原价&emsp;：<b class="price-useless">¥ {{goods.price + 99}}.00</b>
                        </div>
                        <div class="">
                            <b>促销价：</b><b class="price">¥ {{goods.price}}.00</b>
                        </div>
                        <p>库存&emsp;：{{goods.quantity}} 件</p>
                        &emsp;&emsp;{{goods.desc}}
                    </div>
                    <div class="col-12 row btns align-items-end justify-content-center">
                        <div class="col-4 nopadding">
                            <button class="col btn btn-true" type="button">立即购买</button>
                        </div>
                    </div>


                </div>


            </div>

        </div>
    </main-layout>
</template>

<script>
    import MainLayout from '../layouts/Main.vue'
    import '../css/main.css'
    import '../css/detail.css'

    export default {
        components: {
            MainLayout
        },
        data() {
            return {
                apiUrl: 'http://127.0.0.1/goods/',
                goods: {},
            }
        },
        methods: {
            getDetail: async function () {
                const res = await this.$axios.get(`${this.apiUrl}get/${this.$route.params.id}`)
                this.goods = res.data
                if (res.data === null) {
                    this.$router.go(-1)
                }
            }
        },
        created() {
            this.getDetail()
        }
    }
</script>
