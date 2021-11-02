<template>
    <div>
        <template v-if="status == true">
            <img :src="img" :alt="nombre">
            <p class="text-center">{{nombre}}</p>
        </template>
        <template v-else>
            <img class="gray" :src="img" :alt="nombre">
            <p class="text-center">????????</p>
        </template>
    </div>
</template>

<script>
export default {
    name:'Pokemon',
    props: ['nombre', 'img', 'status']
}
</script>

<style scoped>
    *{
        border-radius: 10px;
        font-size: 25px;
        background: rgb(112, 112, 112);
    }
    img{
        width: 220px;
    }
    .gray{
        filter: grayscale(100%);
    }
</style>