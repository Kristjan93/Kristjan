<template>

    <div class="the-content-housing">
        <h2 class="the-title">
            <span class="the-cool-thing">(</span>
                The wheel
            <span class="the-cool-thing">)</span>
        </h2>
        <div class="the-wheel-container">
                <svg  
                    class="the-wheel"
                    :class="{ 'kick-in' : startAnimation }" 
                    version="1.1" 
                    baseProfile="full" 
                    xmlns="http://www.w3.org/2000/svg">
                    <circle class="the-wheel-circle" cx="25" cy="25" r="25"  />
                    <line class="the-wheel-line" x1="25" y1="25" x2="25" y2="50" />
                </svg>
                <svg 
                    class="the-wheel abs"
                    version="1.1" 
                    baseProfile="full" 
                    xmlns="http://www.w3.org/2000/svg">
                    <circle class="the-wheel-circle" cx="25" cy="25" r="25" />
                    <line class="the-wheel-line" x1="25" y1="25" x2="25" y2="50" />
                </svg>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.the-content-housing {
    max-width: 660px;
    margin: 0 auto;

    .the-title {
        color: #FFFFFA;
        font-family: 'Amatic SC', cursive;
        font-weight: bold;
        font-size: 32px;
        margin: 0;
        padding: 0;
        text-align: left;
        margin-bottom: 10px;
    }

    .the-cool-thing {
        color: #FFFFFA;
        font-family: 'Beth Ellen', cursive;
        font-size: 26px;
    }
}

.the-wheel-container {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: flex-start;
    border-bottom: 1px solid black;

    .the-wheel {
        transition: transform 2s linear;
        height: 50px;
        width: 50px;

        .the-wheel-circle {
            fill: #080708;
        }
        .the-wheel-line {
            stroke: #FFFFFA;
            stroke-width:2;
        }

        &.kick-in {
            transform: translateX(610px) rotate(1398deg);
        }

        &.abs {
            position: absolute;
            fill: blue;
            z-index: -10;
        }
    }
}
</style>

<script>

export default {
    data: () => ({
        startAnimation: false,
    }),
    created() {
        setTimeout(() => {
            this.startAnimation = true;
        }, 100)
    }
}
</script>