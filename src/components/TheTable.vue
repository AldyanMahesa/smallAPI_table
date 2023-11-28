<script setup>
</script>

<template>
  <div v-if="isLoaded">
    <div class="refresh"><button type="button" class="btn btn-danger" @click="reLoad()">refresh</button></div>
    <div class="card" >
    <div class="card-body">
      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Country</th>
            <th scope="col">Name</th>
            <th scope="col">Common Name</th>
            <th scope="col">primary vehicle type</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in Results">
            <th scope="row">{{ item.Mfr_ID }}</th>
            <td>{{item.Country}}</td>
            <td>{{item.Mfr_Name}}</td>
            <td>{{ item.Mfr_CommonName }}</td>
            <td style="font-size: smaller;">
              <div v-for="Type in item.VehicleTypes" >
                <div v-if="Type.IsPrimary == true">
                  <input class="form-check-input" type="checkbox" value='' id="flexCheckDisabled" checked disabled>
                  <label class="form-check-label" for="flexCheckDisabled">
                    {{ Type.Name }}
                  </label>
                </div>
                <div v-if="Type.IsPrimary == false">
                  <input class="form-check-input" type="checkbox" value='' id="flexCheckDisabled" disabled>
                  <label class="form-check-label" for="flexCheckDisabled">
                    {{ Type.Name }}
                  </label>
                </div>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  </div>
  <div class="card" v-if="isLoaded==false && urlResponse != null">
   
    <div class="retry-card"> <div>{{ urlResponse }}</div>
      <button type="button" class="btn btn-danger" @click="reLoad()">Retry</button></div>
  </div>
</template>
<style>
.refresh {
  text-align: right;
}
.retry-card {
  text-align: center;
  margin: 25px 100px 25px;
}
.button{
 margin: 25px 100px 25px;
}
</style>
<script>
import axios from 'axios'

export default {
  name: "Table",
  data() {
    return {
      urlResponse: {},
      Results: [],
      isLoaded: false,
    };
  },
  methods: {
    reLoad(){
      this.LoadTable();
    },
    async LoadTable() {
        await axios.get('https://vpic.nhtsa.dot.gov/api/vehicles/getallmanufacturers?format=json').then(response => {
        this.urlResponse = response;
        this.Results = response.data.Results;
        this.isLoaded = true;
      }).catch(error => {
        console.log(error);
        this.urlResponse = error,
        this.isLoaded = false;
      });
    },
  },
  beforeMount() {
    this.LoadTable();
  },
};
</script>