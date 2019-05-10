<template>
    <div class="content">
        <router-view></router-view>
    </div>
</template>

<script>
export default {
    name: 'Content'
}
</script>

<style>
    .content {
        grid-area: content;

        /*Cor de fundo do template principal*/
        background-color: #e9e9e9;
        padding: 20px;
    }
</style>
