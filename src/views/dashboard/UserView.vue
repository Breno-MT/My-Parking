<template>

    <div class="container mt-5">

        <h1>Novo Usuário</h1>
        <form @submit.prevent="save">
            <div class="row">
                <div class="col-3">
                    <label for="">Nome</label>
                    <input type="text" class="formcontrol" v-model="user.name">
                </div>
                <div class="col-3">
                    <label for="">E-mail</label>
                    <input type="text" class="formcontrol" v-model="user.email">
                </div>
                <div class="col-3">
                    <label for="">Senha</label>
                    <input type="password" class="formcontrol" v-model="user.password">
                </div>
                <div class="col-12 mt-2">
                    <button type="submit" class="btn btn-primary">Salvar</button>
                </div>
            </div>
            
            <router-link to="/">Home</router-link>
        </form>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                user: {},
            }
        },
        methods: {
            save() {
                this.$store.dispatch('userModule/newUser', this.user);
                this.user = {};
            }
        }
    }


</script>