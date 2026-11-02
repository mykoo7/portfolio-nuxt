
<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'

// REFERENCES TO THE CHART CONTAINERS
const distributionElement = ref(null)
const proficiencyElement = ref(null)

const selectedCategory = ref('All')

// STORE THE CHART INSTANCES
let distributionChart = null
let proficiencyChart = null

// TECHNOLOGY DISTRIBUTION DATA
const distributionData = [
  { name: 'Languages', value: 4 },
  { name: 'Databases', value: 2 },
  { name: 'Tools', value: 4 }
]

// TECHNOLOGY PROFICIENCY DATA
const proficiencyData = [
  { name: 'Java', level: 'Developing', value: 50, category: 'Languages' },
  { name: 'HTML', level: 'Advanced', value: 90, category: 'Languages' },
  { name: 'CSS', level: 'Advanced', value: 90, category: 'Languages' },
  { name: 'JavaScript', level: 'Intermediate', value: 70, category: 'Languages' },
  { name: 'PostgreSQL', level: 'Intermediate', value: 70, category: 'Databases' },
  { name: 'MongoDB', level: 'Intermediate', value: 70, category: 'Databases' },
  { name: 'Git', level: 'Intermediate', value: 70, category: 'Tools' },
  { name: 'GitHub', level: 'Advanced', value: 90, category: 'Tools' },
  { name: 'VS Code', level: 'Advanced', value: 90, category: 'Tools' },
  { name: 'Android Studio', level: 'Advanced', value: 90, category: 'Tools' }
]

const filteredData = computed(() => {
    if (selectedCategory.value == 'All') {
        return proficiencyData
    }

    return proficiencyData.filter(item => {
        return item.category == selectedCategory.value
    })
})

let echarts

function updateProficiencyChart() {
    if (!proficiencyChart) return

    proficiencyChart.setOption({
        yAxis: {
            data: filteredData.value.map(tech => tech.name)
        },

        series: [
            {
                data: filteredData.value.map(tech => tech.value)
            }
        ]
    })
}

watch(selectedCategory, () => {
    updateProficiencyChart()
})

// INITIALIZE THE CHARTS
onMounted(async () => {
  // LOAD ECHARTS IN THE BROWSER
  echarts = await import('echarts')

  // INITIALIZE DISTRIBUTION CHART
  distributionChart = echarts.init(distributionElement.value)

  distributionChart.setOption({
    tooltip: {
      trigger: 'item',
      formatter: '{b}: {c} technologies ({d}%)'
    },

    legend: {
      bottom: 0,
      textStyle: {
        color: '#4C0519'
      }
    },

    series: [
      {
        name: 'Technology Distribution',
        type: 'pie',
        radius: ['50%', '70%'],
        center: ['50%', '45%'],

        data: distributionData,

        itemStyle: {
          borderRadius: 8,
          borderColor: '#ffffff',
          borderWidth: 2
        },

        label: {
          show: true,
          position: 'outside',
          color: '#4C0519',
          formatter: '{b}',
          distanceToLabelLine: 5
        },
        labelLine: {
            show: true,
            length: 12,
            length2: 15
        },

        avoidLabelOverlap: false
      }
    ],

    color: ['#9F1239', '#E11D48', '#FDA4AF'],

    media: [
        {
            query: {
                maxWidth: 600
            },
            option: {
                series: [
                    {
                        center: ['50%', '45%'],
                        radius: ['40%', '60%'],

                        label: {
                            show: true,
                            fontSize: 10,
                            distanceToLabelLine: 2
                        },

                        labelLine: {
                            length: 8,
                            length2: 8
                        }
                    }
                ]
            }
        }
    ]

  })

  // INITIALIZE PROFICIENCY CHART
  proficiencyChart = echarts.init(proficiencyElement.value)

  proficiencyChart.setOption({
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'shadow'
      },
      formatter: (params) => {
        const item = filteredData.value.find(
          tech => tech.name === params[0].name
        )

        return `${item.name}<br/>
                Level: ${item.level}<br/>
                Score: ${item.value}/100`
      }
    },

    grid: {
      left: '5%',
      right: '10%',
      bottom: '5%',
      top: '5%',
      containLabel: true
    },

    xAxis: {
      type: 'value',
      min: 0,
      max: 100,
      axisLabel: {
        color: '#4C0519'
      }
    },

    yAxis: {
      type: 'category',
      data: proficiencyData.map(tech => tech.name),
      axisLabel: {
        color: '#4C0519'
      }
    },

    series: [
      {
        name: 'Self-assessed familiarity',
        type: 'bar',

        data: proficiencyData.map(tech => tech.value),

        itemStyle: {
          color: '#BE185D',
          borderRadius: [0, 8, 8, 0]
        },

        barWidth: '55%'
      }
    ]
  })

  // MAKE CHARTS RESPONSIVE
  window.addEventListener('resize', resizeCharts)
})

// RESIZE BOTH CHARTS
function resizeCharts() {
  distributionChart?.resize()
  proficiencyChart?.resize()
}

// CLEAN UP WHEN COMPONENT IS REMOVED
onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeCharts)

  distributionChart?.dispose()
  proficiencyChart?.dispose()
})
</script>

<template>
  <div class="grid grid-cols-1 lg:grid-cols-[1.2fr_1fr] gap-10 lg:gap-20 mt-8 px-4 lg:px-8">

    <!--TECHNOLOGY DISTRIBUTION-->
    <div>
      <h2 class="text-2xl text-center text-rose-950 font-extrabold">
        Technology Distribution
      </h2>

      <p class="text-rose-900 mb-4">
        An overview of my technologies by category.
      </p>

      <div ref="distributionElement" class="w-full min-w-0 h-[450px]"></div>
    </div>

    <!--TECHNOLOGY PROFICIENCY-->
    <div>
      <h2 class="text-2xl text-center text-rose-950 font-extrabold">
        Technology Proficiency
      </h2>

      <p class="text-rose-900 mb-4">
        Self-assessed familiarity with each technology.
      </p>

      <div class="flex flex-wrap justify-center gap-3 mb-6">
        <button
        v-for="category in ['All', 'Languages', 'Databases', 'Tools']"
        :key="category"
        @click="selectedCategory = category"
        :class="['btn btn-sm border-rose-950 transition-all duration-300',
            selectedCategory === category
            ? 'bg-rose-950 text-white'
            : 'bg-transparent text-rose-950 hover:bg-rose-900 hover:text-white'
        ]"> {{ category }}
        </button>
      </div>

      <div
        ref="proficiencyElement"
        class="w-full min-w-0 h-[400px] sm:h-[450px]"></div>
    </div>

  </div>
</template>
