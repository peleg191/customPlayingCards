<template>
    <div>
        <h1>Hover to flip</h1>
        <div :style="computedCardStyle" 
             :class="computedCardClass"
              class="card">
            <div class="card__inner">
                <div class="card__front" :style="computedFrontStyle"></div>
                <card-custom-back-component :back-color="backColor"
                                            :current-back="currentBack"
                                            :height="computedCardHeight"
                                            :width="computedCardWidth"></card-custom-back-component>
            </div>
        </div>
    </div>
</template>
<script>
import cardCustomBackComponent from './card-custom-back-component.vue';
export default {
    name: 'card-component',
    props:['cardHeight',
            'cardWidth',
            'ratio',
            'currentCard',
            'currentShape',
            'currentBack',
            'backColor'],
    components:{cardCustomBackComponent},
    data(){
        return{
            flipCardFlag:false
        }
    },
    watch:{
        currentCard(){
            this.flipCardFlag = true;
            setTimeout(()=>{this.flipCardFlag = false},2500);
        }
    },
    computed:{
        computedRatio(){
            return this.ratio || 1.438;
        },
        computedCardHeight(){
            return (this.cardHeight || 292);
        },
        computedCardHeightPixel(){
            return this.computedCardHeight + 'px';
        },
        computedCardWidth(){
            return this.computedCardHeight / this.computedRatio;
        },
        computedCardWidthPixel(){
            return this.computedCardWidth + 'px';
        },
        computedCardStyle(){
            return {
                '--card-height': this.computedCardHeightPixel,
                '--card-width': this.computedCardWidthPixel
            }
        },
        computedFrontStyle(){
            const result = `/${this.currentCard}_${this.computedShape}.svg`;
            const finalResult = `url(${result})`;
            return {'--my-front':finalResult};
        },
        // computedBackStyle(){
        //     const result = `/backDesigns/${this.computedBack}`;
        //     const finalResult = `url(${result})`;
        //     return {'--my-back':finalResult};
        // },
        computedCardClass(){
            return this.flipCardFlag ? 'need__hover' : ''; 
        },
        computedShape(){
            return this.currentShape || 'clover';
        },
        computedBack(){
            return this.currentBack || '1.svg';
        }
    }
}
</script>
<style scoped>
h1 {
    text-align: center;
    margin-bottom: 2rem;
    font-family: "Oswald", sans-serif;
    font-size: 2rem;
    color: #f1c40f;
    text-transform: uppercase;
}

.card {
    display: block;
    width: var(--card-width);
    height: var(--card-height);
    perspective: 1000px;
}

.card:hover .card__inner {
    transform: rotateY(-180deg);
} 
.need__hover .card__inner {
    transform: rotateY(-180deg);
}

.card__inner {
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.5s ease-in-out;
    transform-style: preserve-3d;
    box-shadow: -10px 2px 10px 1px rgba(0,0,0,0.5);
    border-radius: 0.5rem;
}


.card__front {
    transform: rotateY(-180deg);
    background: var(--my-front);
    background-repeat: no-repeat;
    background-size: cover;
    height: 100%;
    width: 100%;
    position: absolute;
}
</style>