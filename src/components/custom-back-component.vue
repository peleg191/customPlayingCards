<template>
    <div>
        <div class="row">
            <div class="title">Design</div>
        </div>
        <div class="row mt-2">
            <div class="card my-design"  @click="chooseBack(1)">
                <back_1 :color="backColor"></back_1>
            </div>
            <div class="card my-design"  @click="chooseBack(2)" >
                <back_2 :color="backColor"></back_2>
            </div>
            <div class="card my-design"  @click="chooseBack(3)">
                <back_3 :color="backColor"></back_3>
            </div>
        </div>
        <div class="row">
            <div class="title">Color</div>
        </div>
        <div class="row mt-2">
            <input type="color" v-model="backColor" />
        </div>
    </div>
</template>
<script>
import back_1 from './dynamic_svgs/back_1.vue';
import back_2 from './dynamic_svgs/back_2.vue';
import back_3 from './dynamic_svgs/back_3.vue';
const designs = { 1: 'back_1', 2: 'back_2', 3: 'back_3' };
export default {
    name: 'custom-back-component',
    components:{back_1,back_2,back_3},
    data(){
        return{
            backColor:''
        }
    },
    methods: {
        chooseBack(i){
            this.$emit('choose-back',{'component':designs[i],color:this.backColor});
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
.mt-2{
    margin-top:4px;

}
.title{
    text-align: center;
    font-family: "Oswald", sans-serif;
    font-size: 1.5rem;
    color: #f1c40f;
}
</style>