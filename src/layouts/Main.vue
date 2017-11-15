<template>
    <div>
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <a class="navbar-brand" href="#">APP</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
                    aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item active">
                        <router-link class="nav-link" to="/">Home <span class="sr-only">(current)</span></router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" to="/signIn">Sign in</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" to="/signUp">Sign up</router-link>
                    </li>
                    <li class="nav-item dropdown" v-show="logged">
                        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button"
                           data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                            {{username}}
                        </a>
                        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                            <a class="dropdown-item" href="#">Action</a>
                            <a class="dropdown-item" href="#">Another action</a>
                            <div class="dropdown-divider"></div>
                            <a class="dropdown-item" href="#">Something else here</a>
                        </div>
                    </li>
                </ul>
                <form class="form-inline my-2 my-lg-0">
                    <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
                    <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
                </form>
            </div>
        </nav>

        <slot></slot>
    </div>
</template>

<script>
    import VLink from '../components/VLink.vue'

    export default {
        components: {
            VLink
        },
        data() {
            return {
                username: '',
                logged: false,
                apiUrl: "http://127.0.0.1/user/"
            }
        },
        methods: {
            getLogged:async function () {
//                this.$http.get(`${this.apiUrl}logged`).then((res) => {
//                    //console.log("data.logged="+res.data)
//                    this.logged = res.data;
//                    console.log("this.logged="+this.logged)
//                })
                this.logged = await this.$http.get(`${this.apiUrl}logged`);
                console.log("this.logged="+this.logged)
            }
        },
        created() {
            this.getLogged()
        }
    }
</script>

<style scoped>

</style>