<template>
  <div class="bg-gray-100">
    <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8 h-screen">
      <div class="bg-gray-100 grid grid-rows-2 md:grid-rows-1 grid-flow-col gap-4 p-1">
        <div class="chart-container col-span-3 row-span-1 md:col-span-1 bg-white shadow overflow-hidden sm:rounded-lg">
            <div>
                <span class="text-gray-700 block px-3 py-2 text-base font-medium">
                    Why do you create a startup?
                </span>
                <span class="text-gray-500 block px-3 py-2 text-sm font-medium">
                    Trends
                </span>
            </div>
            <PieChart
            :data="chartData"
            :options="options"
            />
        </div>
        <DataTable
          :data="data"
          class="row-span-1 col-span-3 md:row-span-1 md:col-span-3 bg-white shadow overflow-hidden sm:rounded-lg w-full"
        />
      </div>
    </div>
  </div>
</template>

<script>
import PieChart from "../Components/Chart";
import DataTable from "../Components/DataTable";

export default {
  name: "app",
  components: { PieChart, DataTable },
  data() {
    return {
      chartData: {
        hoverBackgroundColor: "red",
        hoverBorderWidth: 10,
        labels: [],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ["#41B883", "#E46651", "#00D8FF"],
            data: [],
          },
        ],
      },
      options: {
        borderWidth: "10px",
        hoverBackgroundColor: "red",
        hoverBorderWidth: "10px",
        responsive: true,
        maintainAspectRatio: false,
      },
      data: []
    };
  },
  async mounted() {
    try {
      // Users
      const userResponse = await fetch("/api/users");
      
      const { users } = await userResponse.json();
      
      const dataUsers = await users.map((elem) => {
        return { ...elem };
      });

      this.data = dataUsers;

      // Reports
      const reportResponse = await fetch("/api/reports");

      const { reports } = await reportResponse.json();

      const dataReceived = await reports.map((elem) => {
        return { ...elem };
      });
      const labelsArr = dataReceived.map((elem) => elem.category);
      const datasetArr = dataReceived.map((elem) => elem.total);

      this.chartData.labels = labelsArr;
      this.chartData.datasets[0].data = datasetArr;
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
