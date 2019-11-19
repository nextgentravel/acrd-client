<template>
  <div class="main">
    <h4>{{ msg }}</h4>
    <p class="lead">Type in any destination in Canada to find the current hotel city rate limits</p>
    <div v-if="loading">
          <div class="spinner"></div>
    </div>
    <autocomplete
      v-if="!loading"
      placeholder="Search ACRD"
      aria-label="Search ACRD"
      style="text-align: left;"
      :search="search"
      :get-result-value="getResultValue"
      @submit="handleSubmit"
      auto-select
    ></autocomplete>
    <br><br>
    <div v-if="result">
      <p><b>January:</b> {{this.result['January']}}</p>
      <p><b>February:</b> {{this.result['February']}}</p>
      <p><b>March:</b> {{this.result['March']}}</p>
      <p><b>April:</b> {{this.result['April']}}</p>
      <p><b>May:</b> {{this.result['May']}}</p>
      <p><b>June:</b> {{this.result['June']}}</p>
      <p><b>July:</b> {{this.result['July']}}</p>
      <p><b>August:</b> {{this.result['August']}}</p>
      <p><b>September:</b> {{this.result['September']}}</p>
      <p><b>October:</b> {{this.result['October']}}</p>
      <p><b>November:</b> {{this.result['November']}}</p>
      <p><b>December:</b> {{this.result['December']}}</p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Calculator',
  props: {
    msg: String
  },
  created () {
    this.fetchData()
  },

 methods: {
    fetchData () {
      this.error = this.post = null
      this.loading = true
      fetch('https://acrd-api.herokuapp.com/cities')
        .then(response => response.json())
        .then(data => {
          this.loading = false
          this.cities = data.citiesList
          this.cityLookup = data.suburbCityList
        })
    },
    search(input) {
      if (input.length < 1) { return [] }
      return this.cities.filter(city => {
        return city.toLowerCase()
          .startsWith(input.toLowerCase())
      })
    },
    getResultValue(result) {
      return result
    },
    handleSubmit(result) {
      let city = this.cityLookup[result] || result;
      console.log('CITY: ', city)
      let uri = `https://acrd-api.herokuapp.com/${city.replace('/','sss')}/rules`
      console.log(uri)
      fetch(uri)
        .then(response => response.json())
        .then(data => {
          this.haveResult = true
          this.result = data;
          console.log(data)
        })
    }
  },
  data: function() {
    return {
      loading: false,
      haveResult: false,
      post: null,
      error: null,
      cities: [],
      result: null,
      cityLookup: {},
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.spinner {
  width: 40px;
  height: 40px;
  margin: 10px auto;
  background-color: #333;

  border-radius: 100%;  
  -webkit-animation: sk-scaleout 1.0s infinite ease-in-out;
  animation: sk-scaleout 1.0s infinite ease-in-out;
}

@-webkit-keyframes sk-scaleout {
  0% { -webkit-transform: scale(0) }
  100% {
    -webkit-transform: scale(1.0);
    opacity: 0;
  }
}

@keyframes sk-scaleout {
  0% { 
    -webkit-transform: scale(0);
    transform: scale(0);
  } 100% {
    -webkit-transform: scale(1.0);
    transform: scale(1.0);
    opacity: 0;
  }
}

</style>
