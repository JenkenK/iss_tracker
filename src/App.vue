<template>
  <main>
    <h1>ISS Tracker</h1>
    <!-- <div>{{ this.issUnixTimeStamp }}</div> -->
    <div>Time: {{ this.issTimeStamp }}</div>
    <div>Date: {{ this.issDate }}</div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      issPosition: "",
      issUnixTimeStamp: null,
      issTimeStamp: null,
      issDate: null,
    };
  },
  mounted() {
    setInterval(() => {
      fetch("http://api.open-notify.org/iss-now.json")
        .then((res) => res.json())
        .then((json) => {
          (this.issPosition = json.iss_position),
            (this.issUnixTimeStamp = json.timestamp),
            this.convertUnixTimeStamp();
        });
    }, 3000);
  },
  methods: {
    convertUnixTimeStamp: function () {
      const unixTime = this.issUnixTimeStamp;
      const months_arr = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec",
      ];
      const date = new Date(unixTime * 1000);
      const year = date.getFullYear();
      const month = months_arr[date.getMonth()];
      const day = date.getDate();
      const hours = date.getHours();
      const minutes = "0" + date.getMinutes();
      const seconds = "0" + date.getSeconds();
      const formattedTime =
        hours + ":" + minutes.substr(-2) + ":" + seconds.substr(-2);
      this.issTimeStamp = formattedTime;
      const formattedDate = day + "-" + month + "-" + year;
      this.issDate = formattedDate;
    },
  },
  computed: {},
};
</script>

<style scoped>
main {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  text-align: center;
}
</style>
