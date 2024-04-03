<script setup>
import VueApexCharts from 'vue3-apexcharts'
import {
  useDisplay,
  useTheme,
} from 'vuetify'
import { hexToRgb } from '@layouts/utils'

const vuetifyTheme = useTheme()
const display = useDisplay()

const series = [
  {
    name: `${ new Date().getFullYear() - 1 }`,
    data: [
      25, 
      30,
      28,
      32,
      35,
      40,
      45,
    ],
  },
  
]

const chartOptions = computed(() => {
  const currentTheme = vuetifyTheme.current.value.colors
  const variableTheme = vuetifyTheme.current.value.variables
  const disabledTextColor = `rgba(${ hexToRgb(String(currentTheme['on-surface'])) },${ variableTheme['disabled-opacity'] })`
  
  return {
    bar: {
      chart: {
        stacked: true,
        parentHeightOffset: 0,
        toolbar: { show: false },
      },
      dataLabels: { enabled: false },
      stroke: { width: 6, lineCap: 'round' },
      colors: [
        `rgba(${ hexToRgb(String(currentTheme.primary)) }, 1)`,
        `rgba(${ hexToRgb(String(currentTheme.info)) }, 1)`,
      ],
      legend: { show: false },
      grid: {
        borderColor: disabledTextColor,
        padding: { bottom: 5 },
      },
      plotOptions: {
        bar: {
          borderRadius: 10,
          columnWidth: '30%',
          endingShape: 'rounded',
          startingShape: 'rounded',
        },
      },
      xaxis: {
        axisTicks: { show: false },
        crosshairs: { opacity: 0 },
        axisBorder: { show: false },
        categories: [
          'Lecture Hall A',
          'Lecture Hall B',
          'Lecture Hall C',
          'Lecture Hall D',
          'Lecture Hall E',
          'Lecture Hall F',
          'Lecture Hall G',
        ],
        labels: {
          style: {
            fontSize: '14px',
            colors: disabledTextColor,
            fontFamily: 'Public Sans',
          },
        },
      },
      yaxis: {
        labels: {
          style: {
            fontSize: '14px',
            colors: disabledTextColor,
            fontFamily: 'Public Sans',
          },
        },
      },
    },
  }
})

const roomOccupancyData = [
  {
    icon: 'bx-room',
    occupants: 45,
    hall: 'Lecture Hall G',
    color: 'primary',
  },
  {
    icon: 'bx-room',
    occupants: 40,
    hall: 'Lecture Hall F',
    color: 'info',
  },
]
</script>

<template>
  <VCard>
    <VCardItem class="pb-0">
      <VCardTitle>Lecture Hall Occupancy</VCardTitle>

      <template #append>
        <div class="me-n3">
          <MoreBtn />
        </div>
      </template>
    </VCardItem>

    <!-- bar chart -->
    <VueApexCharts
      id="bar-chart"
      type="bar"
      :height="336"
      :options="chartOptions.bar"
      :series="series"
    />

    <VCardText class="text-center">
      <div class="d-flex align-center justify-center gap-x-8 gap-y-4 flex-wrap">
        <div
          v-for="data in roomOccupancyData"
          :key="data.hall"
          class="d-flex align-center gap-3"
        >
          <VAvatar
            :icon="data.icon"
            :color="data.color"
            size="38"
            rounded
            variant="tonal"
          />

          <div class="text-start">
            <span class="text-sm">{{ data.hall }}</span>
            <h6 class="text-base font-weight-medium">
              {{ data.occupants }} Occupants
            </h6>
          </div>
        </div>
      </div>
    </VCardText>
  </VCard>
</template>
