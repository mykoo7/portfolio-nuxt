
<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'

// MY GITHUB ACCOUNT
const username = 'mykoo7'

// STORING THE RETRIEVED DATA
const events = ref([])
const repositories = ref([])
const lastUpdated = ref(null)

// TRACKING LOADING AND ERRORS
const isLoading = ref(false)
const errorMessage = ref('')

// FETCHING DATA FROM GITHUB
async function fetchGithubData() {
  isLoading.value = true
  errorMessage.value = ''

  try {
    const [eventData, repositoryData] = await Promise.all([
      $fetch(`https://api.github.com/users/${username}/events/public?per_page=100`),

      $fetch(`https://api.github.com/users/${username}/repos?per_page=100`)
    ])

    events.value = eventData
    repositories.value = repositoryData

    lastUpdated.value = new Date()

  } catch (error) {
    console.error('Failed to retrieve GitHub data:', error)

    errorMessage.value =
      'Unable to retrieve GitHub data. Please try again later.'

  } finally {
    isLoading.value = false
  }
}

// FETCHING DATA WHEN THE COMPONENT LOADS
await fetchGithubData()


// SELECTED DATE RANGE
const selectedRange = ref(30)

    //FORMAT DATE TO PH
  function formatDate(date) {
    const year = date.getFullYear()
    const month = String(date.getMonth() + 1).padStart(2, '0')
    const day = String(date.getDate()).padStart(2, '0')

    return `${year}-${month}-${day}`
  }

// GET THE DATES INCLUDED IN THE SELECTED RANGE
const dailyActivity = computed(() => {
  const today = new Date()
  const activity = []

  for (let i = selectedRange.value - 1; i >= 0; i--) {
    const date = new Date(today)
    date.setDate(today.getDate() - i)

    const dateKey = formatDate(date)

    const count = events.value.filter(event => {
      return formatDate(new Date(event.created_at)) === dateKey
    }).length

    activity.push({
      date: dateKey,
      count
    })
  }

  return activity
})

// TOTAL RECORDED ACTIVITIES
const totalActivities = computed(() => {
  return dailyActivity.value.reduce(
    (total, day) => total + day.count, 0
  )
})

// NUMBER OF ACTIVE DAYS
const activeDays = computed(() => {
  return dailyActivity.value.filter(day => day.count > 0).length
})

// MOST ACTIVE DAY
const mostActiveDay = computed(() => {
  if (totalActivities.value === 0) return null

  return dailyActivity.value.reduce((mostActive, day) => {
    return day.count > mostActive.count ? day : mostActive
  }, dailyActivity.value[0])
})

// TOTAL PUBLIC REPOSITORIES
const publicRepositories = computed(() => {
  return repositories.value.length
})

//ECHART LOGICCC
// REFERENCE TO THE CHART CONTAINER
const activityChartElement = ref(null)

// STORE THE CHART INSTANCE
let activityChart = null
let echarts

// INITIALIZE THE ACTIVITY CHART
async function initializeChart() {
  echarts = await import('echarts')

  if (!activityChartElement.value) return

  activityChart = echarts.init(activityChartElement.value)

  updateActivityChart()
}

// UPDATE THE CHART DATA
function updateActivityChart() {
  if (!activityChart) return

  activityChart.setOption({
    tooltip: {
      trigger: 'axis',
      formatter: (params) => {
        const item = params[0]

        return `${item.axisValue}<br/>
                Recorded Activities: ${item.value}`
      }
    },

    grid: {
      left: '5%',
      right: '5%',
      bottom: '12%',
      top: '10%',
      containLabel: true
    },

    xAxis: {
      type: 'category',
      data: dailyActivity.value.map(day => day.date),
      axisLabel: {
        color: '#4C0519',
        rotate: 30
      },
      axisLine: {
        lineStyle: {
          color: '#9F1239'
        }
      }
    },

    yAxis: {
      type: 'value',
      minInterval: 1,
      min: 0,
      axisLabel: {
        color: '#4C0519'
      },
      splitLine: {
        lineStyle: {
          color: '#FDA4AF',
          type: 'dashed'
        }
      }
    },

    series: [
      {
        name: 'Recorded Activities',
        type: 'bar',
        data: dailyActivity.value.map(day => day.count),
        itemStyle: {
          color: '#BE185D',
          borderRadius: [6, 6, 0, 0]
        },
        barMaxWidth: 35
      }
    ]
  })
}

// WATCH FOR DATE RANGE CHANGES
watch(dailyActivity, () => {
  updateActivityChart()
})

// RESIZE THE CHART
function resizeChart() {
  activityChart?.resize()
}

// INITIALIZE AND CLEAN UP
onMounted(() => {
  initializeChart()
  window.addEventListener('resize', resizeChart)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeChart)
  activityChart?.dispose()
})


</script>


<template>
  <div class="w-full px-4 py-8">
    <!--DATE RANGE-->
    <div class="flex flex-col sm:flex-row justify-between items-center gap-4 mb-8">
      <div class="flex flex-wrap justify-center gap-2">
        <button
          v-for="range in [7, 14, 30]"
          :key="range"
          @click="selectedRange = range"
          :class="['btn btn-sm rounded-lg border-rose-950 transition-all duration-300', 
          selectedRange == range
          ? 'bg-rose-950 text-white'
        :'bg-transparent text-rose-950 hover:bg-rose-900 hover:text-white']">
        {{ range }} Days
        </button>
      </div>

      <button
      @click="fetchGithubData"
      :disabled="isLoading"
      class="btn btn-sm bg-rose-900 text-white hover:bg-rose-950 border-none rounded-lg">
      <span v-if="isLoading" class="loading loading-spinner loading-xs"></span>
      <span v-else>Refresh Data</span>
    </button>
    </div>

    <!--LAST UPDATED-->
    <p class="text-xs text-rose-900 text-right mb-5">
      Last Updated:
      {{ lastUpdated ? lastUpdated.toLocaleString() : 'Not yet updated'}}
    </p>

    <!--ERROR MESS-->
    <p v-if="errorMessage" class="text-center text-red-700 mb-4">
      {{ errorMessage }}
    </p>

    <!--SUMMARY CARDS-->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">

      <!--TOTAL ACTIVITIES-->
      <div class="bg-rose-100/20 backdrop-blur-sm border-2 border-rose-400/70 rounded-2xl p-5 shadow-lg shadow-rose-950/20">
        <p class="text-sm text-rose-900">Total Recorded Activities</p>
        <h2 class="text-4xl font-extrabold text-rose-950 mt-3">
          {{ totalActivities }}
        </h2>
      </div>

      <!--ACTIVE DAYS-->
      <div class="bg-rose-100/20 backdrop-blur-sm border-2 border-rose-400/70 rounded-2xl p-5 shadow-lg shadow-rose-950/20">
        <p class="text-sm text-rose-900">Active Days</p>
        <h2 class="text-4xl font-extrabold text-rose-950 mt-3">
          {{ activeDays }}
        </h2>
      </div>

      <!--MOST ACTIVE DAY-->
      <div class="bg-rose-100/20 backdrop-blur-sm border-2 border-rose-400/70 rounded-2xl p-5 shadow-lg shadow-rose-950/20">
        <p class="text-sm text-rose-900">Most Active Day</p>
        <h2 class="text-2xl font-extrabold text-rose-950 mt-3">
          {{ mostActiveDay?.date ?? 'No data' }}
        </h2>
        <p class="text-sm text-rose-900 mt-1">
          {{ mostActiveDay ? `${mostActiveDay.count} activities` : 'No recorded activities' }}
        </p>
      </div>

      <!--PUBLIC REPOSITORIES-->
      <div class="bg-rose-100/20 backdrop-blur-sm border-2 border-rose-400/70 rounded-2xl p-5 shadow-lg shadow-rose-950/20">
        <p class="text-sm text-rose-900">Public Repositories</p>
        <h2 class="text-4xl font-extrabold text-rose-950 mt-3">
          {{ publicRepositories }}
        </h2>
      </div>
    </div>
  </div>
        <!--ECHART DESIGN-->
      <div class="mt-10 w-full bg-rose-100/20 backdrop-blur-sm border-2 border-rose-400/70 rounded-2xl p-5 shadow-lg shadow-rose-950/20">
        <h2 class="text-2xl font-extrabold text-rose-950 text-center">
          Daily Github Activity
        </h2>

        <p class="text-sm text-rose-900 text-center mt-2">
          Number of recorded public activities per day.
        </p>

        <div ref="activityChartElement" class="w-full h-[400px] mt-5">
        </div>
      </div>
</template>

