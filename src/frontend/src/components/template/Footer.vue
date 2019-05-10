<template>
    <footer class="footer">
        <span>Copyright <strong>Mercado UFPB</strong> © 2019 todos os direitos reservados</span>
    </footer>
</template>

<script>
export default {
    name: "Footer"
}
</script>

<style>
    .footer {
        grid-area: footer;
        background-color: rgb(221, 221, 221);
        color: rgb(56, 56, 56);

        display: flex;
        align-items: center;
        justify-content: flex-end;
        padding-right: 10px;
    }
</style>
