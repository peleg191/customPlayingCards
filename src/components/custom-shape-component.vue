<template>
    <div>
        <div v-for="(item, index) in myList" 
            :key="index" 
            class="row my-2 hoverable"
            @click="$emit('choose-shape',item.shape)">
            <div class="col-4">
                <div class="title">
                    {{ item.title }}
                </div>
            </div>
            <div class="col-6">
                <div class="symbol" :style="calcSymbolStyle(item.symbol)">
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'custom-shape-component',
    data() {
        return {
            myList: [
                { title: 'Symbol 1', symbol: 'clover', shape: 'clover' },
                { title: 'Symbol 2', symbol: 'spade',shape:'spade' },
                { title: 'Symbol 3', symbol: 'diamond',shape:'diamond' },
                { title: 'Symbol 4', symbol: 'heart',shape:'heart' }
            ]
        }
    },
    methods: {
        calcSymbolStyle(symbol) {
            return {
                '--my-symbol': `url(/symbols/${symbol}.svg)`
            }
        }
    }
}
</script>
<style scoped>
.symbol {
    height: 39px;
    width: 42px;
    background: var(--my-symbol);
    background-repeat: no-repeat;
    background-size: cover;

}
.title{
    line-height: 40px;
    user-select: none;
}
.row {
    display: flex;
    flex-wrap: wrap;
    flex: 1 1 auto;
}

.col-6 {
    flex: 0 0 50%;
    max-width: 50%;
}

.col-4 {
    flex: 0 0 33.333%;
    max-width: 33.333%;
}

.col-2 {
    flex: 0 0 16.666%;
    max-width: 16.666%;
}

.my-2{
    margin-top:8px;
    margin-bottom:8px;
}
.hoverable:hover{
    animation-name:rowHover;
    animation-fill-mode: forwards;
    animation-iteration-count: 1;
    animation-duration: .5s;
}
@keyframes rowHover {
    from{background:inherit}
    to{background:#ededed}
    
}
</style>