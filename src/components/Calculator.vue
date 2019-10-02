<template>
  <div class="main">
    <h1>{{ msg }}</h1>
    <form>
      <autocomplete
        placeholder="Search ACRD"
        aria-label="Search ACRD"
        style="text-align: left;"
        :search="search"
        :get-result-value="getResultValue"
        @submit="handleSubmit"
      ></autocomplete>
      <br><br>
      <div v-if="result">
        <p><b>January - April:</b><br> {{this.result['01-04']}}</p>
        <p><b>May - August:</b><br> {{this.result['05-08']}}</p>
        <p><b>September - December:</b><br> {{this.result['09-12']}}</p>
      </div>
    </form>
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

      fetch('http://acrd-api.herokuapp.com/cities')
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
      let uri = `http://acrd-api.herokuapp.com/${city.replace('/','sss')}/rules`
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
</style>
