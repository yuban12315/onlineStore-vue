<template>
    <!--登录页-->
    <main-layout>
        <div class="container">
            <div class="col-md-4 col-md-offset-4 col-xs-10 col-xs-offset-1">
                <form name="signInForm" id="signInForm" class="form col-xs-12" ng-submit="submit()">

                    <div class="title col-xs-12">
                        <b class="label- label-active">Sign in</b>
                        <b class="divider">·</b>
                        <b class="label-" ng-click="toSignUp()">Sign Up</b>
                    </div>
                    <fieldset class="col-xs-12">
                        <!--从服务器获取的错误信息-->
                        <div class="alert alert-warning alert-dismissable col-xs-12"
                             v-show="!error.status">
                            <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span
                                    aria-hidden="true">&times;</span></button>
                            <p class="text-center">error.msg</p>
                        </div>
                        <input class="form-control sign-in col-xs-12" type="text" name="username"
                               placeholder="username" v-model="formData.username" required title="username is required">
                        <input class="form-control sign-in col-xs-12" type="password" name="password" placeholder="password" v-model="formData.password" required title="password is required">
                        <button type="button"v-on:click="submit()"
                                class="btn btn-true col-xs-12">Sign in
                        </button>
                    </fieldset>
                </form>
            </div>
        </div>
        {{formData}}
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
                apiUrl:"http;//127.0.0.1/user/"
            }
        },
        methods: {
            warn: function (message, event) {
                // 现在我们可以访问原生事件对象
                if (event) event.preventDefault()
                alert(message)
            },
            submit:function () {
                this.http.post(`${this.apiUrl}login`,this.formData).then((res)=>{

                })
            }
        }
    }
</script>