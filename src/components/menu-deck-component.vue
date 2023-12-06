<template>
    <div class="deck-container">
        <div class="deck">
            <div v-for="i in 13" :key="i">
                <div class="card" :style="calcStyle(i)" @click="chooseCard(i)">
                    <div class="card__inner">
                        <div :style="calcFrontStyle(i)" class="card__front"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'menu-deck-component',
    props:['shape'],
    computed:{
        computedShape(){
            return this.shape || 'clover';
        }
    },
    methods: {
        calcStyle(i) {
            return { '--z-index': i }
        },
        calcFrontStyle(i){
            const result = `/${i}_${this.computedShape}.svg`;
            const finalResult = `url(${result})`;
            return {'--my-front':finalResult};
        },
        chooseCard(i){
            this.$emit('choose-card',i);
        }
    }
}
</script>
<style scoped>
.deck-container {
    position: absolute;
    margin-right: auto;
    margin-left: auto;
    width: 98vw;
    left: 0;
}

.deck {
    display: inline-flex;
}

.card {
    position: relative;
    height: 192px;
    width: 105px;
    z-index: var(--z-index);
    margin: 0;
    padding: 0;
    box-shadow: -10px 2px 10px 1px rgba(0,0,0,0.5);
    text-align: center;
    line-height: 192px;
    margin-left: -32px;
    background: white;
    transition: transform .5s ease-in-out;
    transform-style: preserve-3d;

}


.card:hover  {
    transform:scale(1.25);
}
.card__inner {
    width: 100%;
    height: 100%;
    text-align: center;
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
    background: url(/standart_blue_back.svg);
    background-repeat: no-repeat;
    background-size: cover;

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
    background: var(--my-front);
    background-repeat: no-repeat;
    background-size: cover;
    height: 192px;
    width: 105px;
    position: absolute;
}
</style>