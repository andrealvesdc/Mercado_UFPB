<template>
    <div class="home">
        <PageTitle icon="fa fa-home" main="Mercado UFPB"/>
        <div class="stats">
            
            <!-- estatisticas do sistema --> 
            
            <Stat title="Anúncios cadastrados" :value="stat.articles"
                icon="fa fa-file" color="#3bc480" />
            <Stat title="Usuários cadastrados" :value="stat.users"
                icon="fa fa-user" color="#3282cd" />
        </div>
    </div>
</template>

<script>
import PageTitle from '../template/PageTitle'
import Stat from './Stat'
import axios from 'axios'
import { baseApiUrl } from '@/global'

export default {
    name: 'Home',
    components: { PageTitle, Stat },
    data: function() {
        return {
            stat: {}
        }
    },
    methods: {
        getStats() {
            axios.get(`${baseApiUrl}/stats`).then(res => this.stat = res.data)
        }
    },
    mounted() {
        this.getStats()
    }
}
</script>

<style>
    .stats {
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        color: rgb(47, 67, 105);
    }
</style>
