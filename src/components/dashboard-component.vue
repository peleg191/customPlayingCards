<template>
    <div class="dashboard-body">
        <div class="title">Customization Dashboard</div>
        <div class="tabs">
            <div :class="calcTabClass(1)" class="tab" @click="tab = 1">Shapes</div>
            <div :class="calcTabClass(2)" class="tab" @click="tab = 2">Front</div>
            <div :class="calcTabClass(3)" class="tab" @click="tab = 3">Back</div>
        </div>
        <div class="tab-body">
            <component :is="tabComponent"
                        @choose-shape="$emit('choose-shape',$event)"
                        @choose-back="$emit('choose-back',$event)"></component>
        </div>
    </div>
</template>
<script>
import customShapeComponent from './custom-shape-component.vue';
import customBackComponent from './custom-back-component.vue';
const myTabs = {1:'custom-shape-component',2:'custom-front-component',3:'custom-back-component'};
export default {
    name: 'dashboard-component',
    components:{customShapeComponent,customBackComponent},
    data(){
        return{
            tab:1,
        }
    },
    methods:{
        calcTabClass(i){
            return this.tab == i ? 'active' : '';
        }
    },
    computed:{
        tabComponent(){
            return myTabs[this.tab];
        }
    }
}
</script>
<style scoped>
.title {
    text-align: center;
    font-family: "Oswald", sans-serif;
    font-size: 2rem;
    color: #f1c40f;
    text-transform: uppercase;
}

.dashboard-body {
    height: 55vh;
    width: 75vh;
    background: #fefefe;
    box-shadow:
        0px 11px 15px -7px rgba(0, 0, 0, 0.2),
        0px 24px 38px 3px rgba(0, 0, 0, 0.2),
        0px 9px 46px 8px rgba(0, 0, 0, 0.2);
    left: 5vh;
    top: 12vh;
    position: absolute;
    z-index: 1;
    color: black;
}

.tabs {
    width: 100%;
    height: 5vh;
    background: #282828;
    display: inline-flex;
}

.tab {
    border: 1px solid white;
    width: 25vh;
    line-height: 5vh;
    color: white;
    user-select: none; 
}

.tab:hover {
    animation-name: hoverTabAnimation;
    animation-duration: .5s;
    animation-fill-mode: forwards;
    animation-iteration-count: 1;
}
.tab.active{
    background: #f1c40f;

}

@keyframes hoverTabAnimation {
    from {
        background: inherit;
    }

    to {
        background: #8a8a8a;
    }
}</style>