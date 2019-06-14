<template>
    <svg class="progress" :width="size" :height="size" :viewBox="viewBox">
        <circle class="progress__meter" :cx="size/2" :cy="size/2" :r="radius" :stroke-width="stroke" />
        <circle class="progress__value" :cx="size/2" :cy="size/2" :r="radius" :stroke-width="stroke" :style="progressStyle"/>
    </svg>   
</template>

<script>

export default {
    props: {
        progress: {
            type: Number,
            default: 0,
        },
        size: {
            type: Number,
            default: 120,
        },
        stroke: {
            type: Number,
            default: 12
        }
    },
    data() {
        return {
            delayed: true,
        }
    },
    mounted() {
        setTimeout(() => this.delayed = false, 100);
    },
    computed: {
        circumference() {
            return 2 * Math.PI * this.radius;
        },
        progressStyle() {
            let prog = this.progress;
            if(this.delayed) {
                prog = 0;
            } 

            let dashoffset = this.circumference * (1 - prog);

            return {
                strokeDashoffset: dashoffset,
                strokeDasharray: this.circumference,
            }
        },
        viewBox() {
            return `0 0 ${this.size} ${this.size}`;
        },
        radius() {
            return ( this.size / 2 ) - (this.stroke / 2);
        }
    }
}
</script>

<style lang="scss" scoped>

.progress {
    transform: rotate(-90deg);
}

.progress__meter,
.progress__value {
    fill: none;
}

.progress__meter {
    stroke: #e6e6e6;
}

.progress__value {
    stroke: #f77a52;
    stroke-linecap: round;
    stroke-dashoffset: 0;
    transition: stroke-dashoffset 1s ease-in-out;
}
</style>