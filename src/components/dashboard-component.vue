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
        <div class="row-center">
            <div class="my-button" 
                 :class="savePresetClass"
                 @click="onClickSavePreset">Save Preset</div>
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
            savePresetClass:''
        }
    },
    methods:{
        calcTabClass(i){
            return this.tab == i ? 'active' : '';
        },
        onClickSavePreset(){
            this.savePresetClass = 'button-clicked';
            setTimeout(()=>{this.savePresetClass = '';},500);
            this.$emit('save-preset');
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
    height: 67vh;
    width: 75vh;
    background: #fefefe;
    box-shadow: 0px 11px 15px -7px rgba(0, 0, 0, 0.2),
        0px 24px 38px 3px rgba(0, 0, 0, 0.2),
        0px 9px 46px 8px rgba(0, 0, 0, 0.2);
    left: 5vh;
    top: 1vh;
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
}
.row-center{
    flex-direction: row;
    display: flex;
    justify-content: center;
    position: absolute;
    margin-left: auto;
    margin-right: auto;
    width: 75vh;
    top: 57.5vh;
}
.my-button{    
    font-family: Avenir, Arial, sans-serif;
    font-weight: 900;
    font-size: 1.5rem;
    text-shadow: 0 3px 1px #947704;
    width:180px;
    height:45px;
    border-radius:8px;
    background:gold;
    box-shadow: 0 8px 0 #b18e04, 0 15px 20px rgba(0, 0, 0, 0.35);
    color:white;
    line-height:45px;
    user-select:none;
}

.button-clicked {
    animation-name: animationPressed;
    animation-duration: .5s;
    animation-fill-mode: forwards;
    animation-iteration-count: 1;
    animation-timing-function: ease-in-out;
}

@keyframes animationPressed {
    from {
        padding-top: 0px;
        transform: translateY(0px);
        box-shadow: 0 8px 0 #b18e04, 0 15px 20px rgba(0, 0, 0, 0.35);
    }

    50% {
        padding-top: 2px;
        transform: translateY(2px);
        box-shadow: 0 1px 0 #b18e04, 0 15px 20px rgba(0, 0, 0, 0.35);
    }

    to {
        padding-top: 0px;
        transform: translateY(0px);
        box-shadow: 0 8px 0 #b18e04, 0 15px 20px rgba(0, 0, 0, 0.35);
    }
}
</style>