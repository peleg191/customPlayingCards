<template>
    <div class="card__back">
                    <component :is="finalBack" 
                                :color="backColor"
                                :height="height"
                                :width="width"></component>
    </div>
</template>
<script>
import back_1 from './dynamic_svgs/back_1.vue';
import back_2 from './dynamic_svgs/back_2.vue';
import back_3 from './dynamic_svgs/back_3.vue';
export default {
    name:'card-custom-back-component',
    props:['backColor','currentBack','height','width'],
    components:{back_1,back_2,back_3},
    computed:{
        finalBack(){
            return this.currentBack || 'back_1';
        }
    }
}
</script>
<style scoped>

.card__back {
    width: 100%;
    height: 100%;
    border-radius: 0.5rem;
    position: absolute;
    backface-visibility: hidden;
}

/* .card__back {
    background: var(--my-back);
    background-repeat: no-repeat;
    background-size: cover;
    backface-visibility: hidden;
} */

.card__back:before {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    backface-visibility: hidden;
}
</style>