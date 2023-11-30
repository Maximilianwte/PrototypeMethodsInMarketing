<template>
  <div class="flex flex-col pb-20 justify-center items-center mx-auto px-12 w-full lg:w-3/4">
    <h1 class="col-span-3 w-full mt-12 font-semibold text-blue-500 text-3xl ml-4">Research Visualized</h1>
    <div class="triggerChartType ml-4 mt-4 flex col-span-3 text-xl cursor-pointer w-full">
      <div id="bar" @click="setActiveView('chart')" class="pr-2 py-2 px-2 rounded-tl-xl text-white bg-blue-400 hover:bg-blue-200 hover:text-grey-800">
        Chart view
      </div>
      <div id="line" @click="setActiveView('table')" class="pl-2 py-2 px-2 rounded-tr-xl text-grey-800 bg-blue-200 hover:bg-blue-400 hover:text-white">
        Table view
      </div>
    </div>
    <div v-if="activeView == 'chart'" id="chart" class="col-span-3 mt-6 w-full">
      <apexchart class="w-full" :key="chartKey" :type="activeChart" :options="chartOptions" :series="series"></apexchart>
    </div>
    <div v-if="activeView == 'table'" id="tableView">
      <div id="headerTable" class="text-2xl font-semibold w-full mt-12 mb-2">
      <h2>Publications</h2>
    </div>
    <div id="table" class="w-full">
      <ul>
        <li id="header" class="mb-8">
          <h3 class="text-lg">17,526 articles</h3>
        </li>
        <li v-for="(publication, index) in publicationData" :key="index" class="w-full mb-8">
        <a :href="publication.url" target="_blank" class="col-span-3 text-xl font-medium">
            {{ publication.title }}
            <span class="text-base"> - {{ publication.authors }}</span>
        </a>
        <p class="mb-2">
          {{ publication.year }} - {{ publication.journal }}
            <span class="text-green-600">({{ publication.journal_ranking }})</span>
        </p>
    </li>
      </ul>
    </div>
    </div>


  </div>
</template>

<script>
export default {
  data() {
    return {
      publicationData: [
        {'url': 'https://journals.sagepub.com/doi/full/10.1177/00222437211037258',
        'title': 'The Power of Brand Selfie',
        'authors': 'Hartmann, Heitmann, Schamp, Netzer',
      'year': '2021',
      'journal': 'Journal of Marketing Research',
      'journal_ranking': 'A+',

    },
    {'url': 'https://journals.sagepub.com/doi/full/10.1177/00222437211037258',
        'title': 'Another publication',
        'authors': 'More authors',
      'year': '2020',
      'journal': 'Journal of Marketing',
      'journal_ranking': 'A+',

    }
      ],

      activeChart: 'bar',
      activeView: 'chart',
      chartKey: 0,


      chartOptions: {
        chart: {
          id: 'vuechart-example'
        },
        dataLabels: {
              enabled: true,
            },
        xaxis: {
          categories: [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023],
          title: {
            text: 'NLP Articles',
            style: {
              fontSize: '16px'
            }
          }
        },
        yaxis: {
          title: {
            text: 'Number of Publications',
            style: {
              fontSize: '16px'
            }
          }
        }
      },
      series: [{
        name: 'Publications',
        data: [17, 23, 20, 34, 42, 39, 55, 67, 72, 70, 119, 105, 143, 170]
      }]
    }
  },

  methods: {
    setActiveChart(type) {
      this.activeChart = type;
      this.chartKey++;
    },
    setActiveView(type) {
      this.activeView = type;
      this.chartKey++;
    }
  }
}
</script>
