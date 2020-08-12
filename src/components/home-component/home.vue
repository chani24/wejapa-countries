<template>
    <div id="form">
        <br>
        <div class="header">
            <img src="https://www.wejapa.com/favicon.ico" alt="wejapa logo">
            <h1>WEJAPA COUNTRIES</h1>
            <h3>Where would you like to go.......</h3>
        </div>
<form action="">
    <div class="country-div">
        <label for="countries">Country: </label>
    <select name="countries" id="countries" v-model="currentCountryName" @change="onCountryChange($event)">
        
        <option :value="country" v-for="country in countries" :key="country">{{ country }}</option>
    </select>
    </div><br>

    <div class="state-div">
        <label for="countries">State: </label>
    <select name="countries" id="countries" v-model="currentState" @change="onStateChange($event)">
        <option v-if="errorState" value="" selected> This country has no states</option>
        <option :value="state" v-for="state in states" :key="state">{{ state }}</option>
    </select>
    </div><br>

    <div class="city-div">
        <label for="countries">City: </label>
    <select name="countries" id="countries" v-model="currentCity" >
        <option v-if="errorCity" value="" selected> This state has no cities</option>
        <option v-if="errorState" value="" selected> This country has no cities</option>
        <option :value="city" v-for="city in cities" :key="city">{{ city }}</option>
    </select>
    </div><br>
    

    
</form>

        <div class="selection-details">
            <p class="selected-item">SELECTED COUNTRY : {{ currentCountryName }}</p>
            <p class="selected-item">SELECTED STATE : {{ currentState }}</p>
            <p class="selected-item">SELECTED CITY : {{ currentCity }}</p>
        </div>
        <br>
    </div>

    
</template>
<script>

export default {
    
    data(){
        return {
            allCountries: [],
            countriesDetails: [],
            countries: [],
            states: [],
            stateDetails: [],
            cities: [],
            currentCountryName: "",
            currentCountryDetails: {}, 
            currentState: "",
            currentCity: "",
            errorState: false,
            errorCity: false
        }
    },
      created(){
       this.getCountriesList();
    },
    methods: {
        getCountriesList(){
            this.$http.get('https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries%2Bstates%2Bcities.json')
            .then(
            response=>{
                return response.json()
            }
        )
            .then(res => {
                this.allCountries = res;
                this.countries = this.allCountries.map(country => country.name)
            })
        },

        onCountryChange(event){
            
            this.currentState = "";
            this.currentCity = "";
            const country = event.target.value;
            console.log(this.allCountries)

           this.countriesDetails = this.allCountries.find(countries => countries.name == country)

           if(this.countriesDetails.states){
               this.states = this.countriesDetails.states.map(state => state.name)
           }
           else{
               this.errorState = true;
           }

           
        },

        onStateChange(event){
            this.currentCity = "";
            const state = event.target.value;
           const stateDetails =  this.countriesDetails.states.find(states => states.name == state)
           console.log()
            
            if(stateDetails.cities.length > 0){
                this.cities = stateDetails.cities.map(city => city.name);
            }
            else{
              this.errorCity = true;
            }
            

        },

        
    }
}
</script>
<style scoped>
#form{
    margin: auto;
    padding: 0 0 0 0;
    background-color: rgba(255, 255, 255, 0.911);
}
h1{
    font-weight: 900;
}
h3{
    color: #63c069;
}

select {
    padding: 5px 8px;
    width: 130%;
    box-shadow: none;
    background: transparent;
    -webkit-appearance: none;
    text-align: center;
}

 select:focus {
    outline: none;
}
</style>