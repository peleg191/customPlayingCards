<template>
    <div>
        <div class="row">
            <div class="card my-design" :style="calcStyle(1)" @click="chooseBack(1)"></div>
            <div class="card my-design" :style="calcStyle(2)" @click="chooseBack(2)" ></div>
            <div class="card my-design" :style="calcStyle(3)" @click="chooseBack(3)"></div>
        </div>
        <div class="row">
            <input type="color" v-model="backColor" />
        </div>
    </div>
</template>
<script>
const designs = { 1: '1.svg', 2: '2.svg', 3: '3.svg' };
export default {
    name: 'custom-back-component',
    data(){
        return{
            backColor:''
        }
    },
    methods: {
        calcStyle(i) {
            return { '--my-back': `url(backDesigns/${designs[i]})` }
        },
        chooseBack(i){
            this.$emit('choose-back',designs[i]);
        }
    }
}
</script>

<style scoped>
.card {
    position: relative;
    height: 146px;
    width: 100px;
    z-index: 1;
    margin: 0;
    padding: 0;
    box-shadow: -10px 2px 10px 1px rgba(0, 0, 0, 0.5);
    text-align: center;
    line-height: 192px;
    transition: transform .5s ease-in-out;
    transform-style: preserve-3d;
}
.card:hover{
    animation:hoverAnimation .5s 1;
    animation-fill-mode: forwards;
}
@keyframes hoverAnimation{
    from{opacity:1}
    to{opacity:0.7}
}
.my-design {
    background: var(--my-back);
    background-repeat: no-repeat;
    background-size: cover;
    margin-left:16px;
    margin-right: 16px;
}

.row {
    margin-top:16px;
    flex-direction: row;
    display: flex;
    justify-content: center;
}
</style>