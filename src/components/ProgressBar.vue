<template>
    <div class="progress-container">
        <div class="progress-gauge" :style="gaugeStyle"></div>
    </div>
</template>
<script>
    export default {
        name: 'ProgressBar',
        props: {
            max: {
                type: Number,
                default: 100
            },
            value: {
                type: Number,
                default: 0
            }
        },
        computed: {
            gaugeStyle() {
                return {
                    width: this.gaugePercent + '%',
                    'background-color': this.gaugeColor
                }
            },
            gaugePercent() {
                return this.value / this.max * 100;
            },
            gaugeColor() {
                if (this.gaugePercent <= 33) {
                    return '#ff0000';
                }

                if (this.gaugePercent <= 66) {
                    return 'orange';
                }

                return '#00ff00';
            }
        }
    }
</script>
<style>
    .progress-container {
        width: 100%;
        border: 1px solid black;
    }

    .progress-gauge {
        height: 100%;
    }
</style>