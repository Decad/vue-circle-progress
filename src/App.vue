<template>
    <circle-progress :progress="p" size="120" stroke="8"></circle-progress>
</template>

<script>
import CircleProgress from './Progress.vue';

export default {
    components: { CircleProgress },
    data() {
        return {
            p: 0.25,
        }
    },
    mounted() {
    }
}
</script>
