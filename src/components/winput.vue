<template>
  <div class=container-lg>
    <input v-model="message" id="zipcode" placeholder="zipcode goes here" />
    <br />
    <div class="btn-group" role="group" aria-label="Basic radio toggle button group">
      <input
        type="radio"
        class="btn-check"
        name="btnradio"
        id="btnradio1"
        autocomplete="off"
        v-model="unit"
        value="imperial"
        checked
      />
      <label class="btn btn-outline-primary" for="btnradio1">Fahrenheit</label>

      <input
        type="radio"
        class="btn-check"
        v-model="unit"
        value="metric"
        name="btnradio"
        id="btnradio2"
        autocomplete="off"
      />
      <label class="btn btn-outline-primary" for="btnradio2">Celsius</label>
    </div>
    <button type="button" class="btn btn-secondary" @click="update()">Submit</button>

    <br />
    <p class="text">It is {{temp}} {{deg}} Outside in {{city}}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "winput",
  props: ["temp", "city", "deg"],
  mounted() {
    axios
      .get(
        "http://api.openweathermap.org/data/2.5/weather?q=65742,us&appid=8e3634e726c8b5e3cfc2c8364f2906b8&units=imperial"
      )
      .then((response) => {
        console.log(response),
          (this.temp = response.data.main.temp),
          (this.city = response.data.name);
      });
  },
  methods: {
    update() {
      //var unit = "imperial"
        axios
          .get(
            "http://api.openweathermap.org/data/2.5/weather?q=" +
              this.message +
              ",us&appid=8e3634e726c8b5e3cfc2c8364f2906b8&units=" +
              this.unit +
              ""
          )
          .then((response) => {
            console.log(response),
            (this.temp = response.data.main.temp),
              (this.city = response.data.name)
          });
        //if (this.unit = "imperial") {this.deg = "Fahrenheit"} else { this.deg = "Celsius"};
    }
  }
};
</script>

<style scoped>
.btn-outline-primary {
  color: white;
}
.text {
  color: white;
}

input {
  size: 120px;
}
</style>