<template>
    <main-layout>

        <div class="row">
            <div class="col-md-3 col-sm-12">
                <div class="choose-list">
                    <h1 class="title">主题市场</h1>
                    <b class="assort" v-on:click="getGoods('all')">全部商品</b>
                    <b class="assort" v-for="item in goodsType">{{item.assort}}</b>
                </div>
            </div>
            <div class="col-sm">
                <div class="goods-list row">
                    <div class="box col-4" v-for="item in goods">
                        <div class="goods " >
                            <img class="center-block" v-bind:src="item.picture" style="display: block;">
                            <h3 class="col price text-center">¥ {{item.price}}.00</h3>
                            <h5 class="col text-center">{{item.name}}</h5>
                            <!--{{item}}-->
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main-layout>
</template>

<script>
    import MainLayout from '../layouts/Main.vue'
    import '../main.css'
    import '../css/home.css'

    export default {
        components: {
            MainLayout
        },
        data() {
            return {
                apiUrl: 'http://127.0.0.1/goods/',
                goods: [],
                page: 0,
                goodsType: [{
                    assort: "手办"
                }, {
                    assort: "航模"
                }, {
                    assort: "枪模"
                }, {
                    assort: "船模"
                }]
            }
        },
        methods: {
            getGoods: async function (assort) {
                const res = await this.$axios.get(`${this.apiUrl}getList/${assort}/${this.page}`)
                this.goods = res.data
                this.goods[2]=res.data[0]
                this.goods[3]=res.data[0]
                this.goods[4]=res.data[0]
                console.log(this.goods)
            }
        },
        created() {
            this.getGoods('all')
        }
    }
</script>
