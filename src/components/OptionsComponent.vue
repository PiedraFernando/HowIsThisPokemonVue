<template>
    <div class="d-flex justify-content-center mt-5">
        <button type="button" class="btn btn-outline-secondary m-2" @click="check1">{{name1}}</button>
        <button type="button" class="btn btn-outline-secondary m-2" @click="check2">{{name2}}</button>
        <button type="button" class="btn btn-outline-secondary m-2" @click="check3">{{name3}}</button>
  </div>
</template>

<script>
export default {
    name:"OptionComponent",
    props:['name1','name2','name3'],
    emits:['check'],
    methods: {
        check1(){
            this.$emit('check', this.name1)
        },
        check2(){
            this.$emit('check', this.name2)
        },
        check3(){
            this.$emit('check', this.name3)
        },
    },
}
</script>