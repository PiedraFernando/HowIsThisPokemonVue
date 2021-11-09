<template>
    <p class="text-center h4">{{title}}</p>
    <div class="number w-100 ">
        <div class="h-100 row">
            <div class="col-4 d-flex justify-content-evenly align-items-center">
                <div v-if="number > 1">
                    <button @click="less" class="border rounded-circle border-white p-1 squere d-flex justify-content-evenly align-items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-chevron-left" viewBox="0 0 16 16">
                            <path fill-rule="evenodd" d="M11.354 1.646a.5.5 0 0 1 0 .708L5.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z"/>
                        </svg>
                    </button>
                </div>
            </div>
            <div class="col-4 d-flex justify-content-evenly align-items-center">
                <p class="h3 rounded-circle bg d-flex justify-content-evenly align-items-center">{{number}}</p>
            </div>
            <div class="col-4 d-flex justify-content-evenly align-items-center">
                <div v-if="number < maxNumber" class="col-4">
                    <button @click="add" class="border rounded-circle border-white p-1 squere d-flex justify-content-evenly align-items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-chevron-right" viewBox="0 0 16 16">
                            <path fill-rule="evenodd" d="M4.646 1.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1 0 .708l-6 6a.5.5 0 0 1-.708-.708L10.293 8 4.646 2.354a.5.5 0 0 1 0-.708z"/>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'NumberComponent',
    props: ['maxNumber','title'],
    emits:['changeNumber'],
    data(){
        return{
            number:1
        }
    },
    methods:{
        less(){
            this.number = this.number - 1
            this.$emit('changeNumber',this.number)
        },
        add(){
            this.number = this.number + 1
            this.$emit('changeNumber',this.number)
        },
        
    }
}
</script>

<style scoped>
    .number{
        height: 60px;
    }
    .squere{
        width: 30px;
        height: 30px;
    }
    .bg{
        width: 45px;
        height: 45px;
        background-color: rgb(107, 107, 107);
    }
</style>