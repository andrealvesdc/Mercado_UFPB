<template>
    <div class="auth-content">
        <div class="auth-modal">
            <img src="@/assets/logo.png" width="200" alt="Logo" />
            <hr>
            <div class="auth-title">{{ showSignup ? 'Cadastro' : 'Login' }}</div>

            <input v-if="showSignup" v-model="user.name" type="text" placeholder="Nome">
            <input v-model="user.email" name="email" type="text" placeholder="E-mail">
            <input v-model="user.password" name="password" type="password" placeholder="Senha">
            <input v-if="showSignup" v-model="user.confirmPassword"
                type="password" placeholder="Confirme a Senha">

            <button type="submit" v-if="showSignup" @click="signup">Registrar</button>
            <button type="submit"  v-else @click="signin">Entrar</button>

            <a href @click.prevent="showSignup = !showSignup">
                <span v-if="showSignup">Já tem cadastro? Acesse o Login!</span>
                <span v-else>primeiro acesso? Cadastre-se!</span>
            </a>
        </div>
    </div>
</template>

<script>
import { baseApiUrl, showError, userKey } from '@/global'
import axios from 'axios'

export default {
    name: 'Auth',
    data: function() {
        return {
            showSignup: false,
            user: {}
        }
    },
    methods: {
        signin() {
            axios.post(`${baseApiUrl}/signin`, this.user)
                .then(res => {
                    this.$store.commit('setUser', res.data)
                    localStorage.setItem(userKey, JSON.stringify(res.data))
                    this.$router.push({ path: '/' })
                })
                .catch(showError)
        },
        signup() {
            axios.post(`${baseApiUrl}/signup`, this.user)
                .then(() => {
                    this.$toasted.global.defaultSuccess()
                    this.user = {}
                    this.showSignup = false
                })
                .catch(showError)
        }
    }
}
</script>

<style>
    .auth-content {
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .auth-modal {
        background-color: #ffffff;
        width: 380px;
        padding: 10px;
        box-shadow: 0 1px 10px rgba(73, 73, 73, 0.3);

        display: flex;
        flex-direction: column;
        align-items: center;
        border-radius: 6px;
    }

    .auth-title {
        font-size: 1.2rem;
        font-weight: 100;
        margin-top: 10px;
        margin-bottom: 10px;
    }

    .auth-modal input[type = "text"],.auth-modal input[type = "password"] {
        border:0;
        background: none;
        display: block;
        margin: 8px auto;
        text-align: center;
        border: 2px solid #3e69a5;
        padding: 14px 10px;
        width: 200px;
        outline: none;
        color: rgb(0, 0, 0);
        border-radius: 10px;
        transition: 0.40s;
        font-size: 16px;
    }

    .auth-modal input[type = "text"]:focus,.auth-modal input[type = "password"]:focus{
        width: 300px;
        border-color:  rgb(50, 98, 255);
    }

    .auth-modal button {
        border:0;
        background: none;
        display: block;
        margin: 40px auto;
        text-align: center;
        border: 2px solid  rgb(7, 112, 231);
        padding: 10px 40px;
        outline: none;
        color: #c7c7c7;
        border-radius: 24px;
        transition: 0.25s;
        cursor: pointer;
        font-size: 16px;

    }

    .auth-modal button[type = "submit"]:hover{
        background:  rgb(7, 112, 231);
        color: rgb(255, 255, 255);
    }

    .auth-modal a {
        margin-top: 15px;
    }

    .auth-modal hr {
        border: 10;
        width: 75%;
        height: 1px;
        background-image: linear-gradient(to right,
            rgba(4, 29, 253, 0),
            rgba(35, 76, 190, 0.75),
            rgba(120, 120, 120, 0));
    }
</style>
