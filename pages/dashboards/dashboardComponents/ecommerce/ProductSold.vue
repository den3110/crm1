<script setup lang="ts">
import { ref } from 'vue';
import { computed } from 'vue';
import { useTheme } from 'vuetify';
const theme = useTheme();
const success = theme.current.value.colors.success;
/* Chart */
const chartOptions = computed(() => {
    return {
        chart: {
            type: 'area',
            height: 83,
            fontFamily: `inherit`,
            toolbar: {
                show: false
            },
            sparkline: {
                enabled: true
            },
            group: 'sparklines'
        },
        colors: [success],
        stroke: {
            curve: 'smooth',
            width: 2
        },
        fill: {
            type: 'solid',
            opacity: 0.05
        },
        markers: {
            size: 0
        },
        tooltip: {
            theme: 'dark',
            x: {
                show: false
            }
        }
    };
});
const Chart = [
    {
        name: '',
        color: success,
        data: [30, 25, 35, 20, 30, 40]
    }
];
</script>
<template>
    <v-card elevation="10" >
        <v-card-item>
            <h6 class="text-subtitle-1 textSecondary">Products</h6>
            <h4 class="text-h4 mt-1">78,298</h4>
        </v-card-item>
        <apexchart class="mt-2" type="area" height="83" :options="chartOptions" :series="Chart"> </apexchart>
    </v-card>
</template>
