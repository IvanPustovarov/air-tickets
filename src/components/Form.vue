<template>
  <div class="Form">
    <div class="direction_input">
      <div class="departure">
        <div :class="{ departure__rendering_hide: !listCity }">
          <div
            class="departure__city"
            v-for="city in cities"
            :key="city.id"
            @click="showList(`listCity`)"
          >
            <div v-if="listCity" @click="getCity(city)">{{ city.name }}</div>
          </div>
        </div>
        <div :class="{ departure__rendering_hide: !listAirpost }">
          <div
            class="departure__airport"
            v-for="(airport, index) in selectedCity.airports"
            :key="index"
            @click="showList(`listAirpost`)"
          >
            <div v-if="listAirpost">
              <div>{{ airport.name }}</div>
            </div>
          </div>
        </div>
        <div class="departure__company"></div>
      </div>
      <div class="arrival">
        <div class="arrival__city"></div>
        <div class="arrival__airport"></div>
        <div class="arrival__company"></div>
      </div>
    </div>
    <div>Select Date</div>
    <div>Add passengers</div>
    <div>Go to ticket</div>
  </div>
</template>

<script>
import createStore from "@/store/index.js";

export default {
  name: "Form",
  components: {},
  data() {
    return {
      index: 0,
      cities: createStore.state.cities,
      listCity: false,
      listAirpost: false,
      allAirports: false,
      citiesAirports: [],
      selectedCity: {},
    };
  },
  methods: {
    getCity(city) {
      this.selectedCity = city;
      console.log(this.selectedCity);
    },
    showList(argument) {
      if (argument === "listCity") this.listCity = !this.listCity;
      if (argument === "listAirpost") this.listAirpost = !this.listAirpost;
    },
    showAllAirports(citiesAirports) {
      this.citiesAirports = citiesAirports.airports;
      this.allAirports = !this.allAirports;
    },
  },
};
</script>

<style>
.direction_input {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.departure {
  width: 6rem;
  height: 10rem;
  padding-right: 1rem;
}

.departure__rendering_hide {
  overflow: hidden;
  width: 6rem;
  height: 2rem;
  margin-bottom: 1rem;
}

.departure__city {
  width: 6rem;
  height: 2rem;
  color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(7, 88, 88);
}
.departure__city:hover {
  outline: 2px solid white;
}

.departure__airport {
  width: 6rem;
  height: 2rem;
  color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(69, 83, 18);
}
.departure__airport:hover {
  outline: 2px solid white;
}

.departure__airport__name {
}

.departure__company {
  width: 6rem;
  height: 2rem;
  background-color: rgb(158, 69, 194);
}

.arrival {
  width: 6rem;
  height: 10rem;
  padding-left: 1rem;
}
.arrival__city {
  width: 6rem;
  height: 2rem;
  background-color: rgb(7, 88, 88);
}

.arrival__airport {
  width: 6rem;
  height: 2rem;
  background-color: rgb(158, 192, 36);
}

.arrival__company {
  width: 6rem;
  height: 2rem;
  background-color: rgb(158, 69, 194);
}
</style>
