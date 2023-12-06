<template>
    <div>
        <h1>Hover to flip</h1>
        <div :style="computedCardStyle" 
             :class="computedCardClass"
              class="card">
            <div class="card__inner">
                <div class="card__front" :style="computedFrontStyle"></div>
                <div class="card__back" :style="computedBackStyle"></div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'card-component',
    props:['cardHeight',
            'cardWidth',
            'ratio',
            'currentCard',
            'currentShape',
            'currentBack'],
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
        computedCardWidth(){
            return this.computedCardHeight / this.computedRatio;
        },
        computedCardStyle(){
            return {
                '--card-height':this.computedCardHeight + 'px',
                '--card-width': this.computedCardWidth + 'px'
            }
        },
        computedFrontStyle(){
            const result = `/${this.currentCard}_${this.computedShape}.svg`;
            const finalResult = `url(${result})`;
            return {'--my-front':finalResult};
        },
        computedBackStyle(){
            const result = `/backDesigns/${this.computedBack}`;
            const finalResult = `url(${result})`;
            return {'--my-back':finalResult};
        },
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

.card__back {
    width: 100%;
    height: 100%;
    border-radius: 0.5rem;
    position: absolute;
    backface-visibility: hidden;
}

.card__back {
    /* background-color: #fff;
  background-image: repeating-linear-gradient(135deg, #2980b9, #2980b9 5px, transparent 6px, transparent 11px, #2980b9 12px, #2980b9 12px, transparent 13px, transparent 18px), repeating-linear-gradient(45deg, #2980b9, #2980b9 5px, transparent 6px, transparent 11px, #2980b9 12px, #2980b9 12px, transparent 13px, transparent 18px);
  box-shadow: inset 0 0 0 10px #fff, inset 0 0 0 20px #2980b9, inset 0 0 0 22px #fff, inset 0 0 0 18px #2980b9; */
    background: var(--my-back);
    background-repeat: no-repeat;
    background-size: cover;
    backface-visibility: hidden;


}

.card__back:before {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    backface-visibility: hidden;
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