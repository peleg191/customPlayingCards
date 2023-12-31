<template>
    <div class="deck-container">
        <div class="deck">
            <div v-for="i in 13" :key="i">
                <div class="card" :style="calcStyle(i)" @click="chooseCard(i)" :class="deckClass">
                    <div class="card__inner">
                        <div :style="calcFrontStyle(i)" class="card__front" :class="frontClass"></div>
                        <card-custom-back-component :back-color="backColor" :current-back="currentBack" :height="160"
                            :width="110"></card-custom-back-component>
                    </div>
                </div>
            </div>
        </div>
        <div class="animation-btn" :class="animationButtonClass" @click="onClickAnimationButton">
            <span>Flip!</span>
        </div>
    </div>
</template>
<script>
import cardCustomBackComponent from './card-custom-back-component.vue';
export default {
    name: 'menu-deck-component',
    components: { cardCustomBackComponent },
    props: ['shape', 'currentBack', 'backColor'],
    data() {
        return {
            deckClass: '',
            frontClass: '',
            rotationDeg: 180,
            animationButtonClass: ''
        }
    },
    computed: {
        computedShape() {
            return this.shape || 'clover';
        }
    },
    methods: {
        calcStyle(i) {
            return { '--z-index': i, '--my-transition-delay': ((i * 0.1) - 0.1) + 's', 
                    '--my-rotation': `rotateY(${this.rotationDeg}deg)`,
                    '--my-hover-transition':`scale(1.25) rotateY(${360-parseInt(this.rotationDeg)}deg)` };
        },
        calcFrontStyle(i) {
            const result = `/${i}_${this.computedShape}.svg`;
            const finalResult = `url(${result})`;
            return { '--my-front': finalResult };
        },
        chooseCard(i) {
            this.$emit('choose-card', i);
        },
        onClickAnimationButton() {
            this.deckClass = 'animate-card';
            this.rotationDeg += 180;
            this.frontClass = 'animate-front';
            this.animationButtonClass = 'button-pressed';
            setTimeout(()=>{this.animationButtonClass = ''},1000);
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
    height: 160px;
    width: 110px;
    z-index: var(--z-index);
    margin: 0;
    padding: 0;
    box-shadow: -10px 2px 10px 1px rgba(0, 0, 0, 0.5);
    text-align: center;
    line-height: 192px;
    margin-left: -32px;
    background: white;
    transition: transform .15s ease-in-out;
    transform-style: preserve-3d;
    perspective: 1000px;
    display: block;
    transform: rotateY(180deg);


}

.animation-btn {
    border-radius: 50%;
    width: 150px;
    height: 150px;
    border: none;
    color: white;
    font-family: Avenir, Arial, sans-serif;
    font-weight: 900;
    font-size: 2.5rem;
    background: #f1c40f;
    text-shadow: 0 3px 1px #947704;
    box-shadow: 0 8px 0 #b18e04, 0 15px 20px rgba(0, 0, 0, 0.35);
    text-transform: uppercase;
    transition: 0.4s all ease-in;
    outline: none;
    cursor: pointer;
    text-align: center;
    user-select: none;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
    left: 85vw;
    top: 0vh;
    position: absolute;
}

.animation-btn span {
    position: relative;
    line-height: 150px;
}

/* fix for IE 11 (and IE8+, although the earlier versions are harder to address) stupidly moving the inner button text on click */
.pressed {
    padding-top: 2px;
    transform: translateY(2px);
    box-shadow: 0 1px 0 #b18e04, 0 15px 20px rgba(0, 0, 0, 0.35);
}

.card:hover {
    transform: var(--my-hover-transition);
    transition-duration: 0.25s;
    transition-timing-function:ease-in-out;

}

.animate-card {
    transition-delay: var(--my-transition-delay);
    transition-duration: 1.2s;
    transform: var(--my-rotation);
}

.card__inner {
    width: 100%;
    height: 100%;
    text-align: center;
    transform-style: preserve-3d;
    box-shadow: -10px 2px 10px 1px rgba(0, 0, 0, 0.5);
    border-radius: 0.5rem;
}


.card__front {
    background: var(--my-front);
    transform: rotateY(180deg);
    background-repeat: no-repeat;
    background-size: cover;
    height: 100%;
    width: 100%;
    position: absolute;
}

.button-pressed {
    animation-name: animationPressed;
    animation-duration: .75s;
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
}</style>