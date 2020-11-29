<template>
    <div class="image-container" :class="weatherClass">
        <main class="main-container">
            <search @set-weather="setWeather"></search>
            <weather-info :weather="weather"></weather-info>
        </main>
    </div>
</template>

<script>
import Search from './components/Search.vue';
import WeatherInfo from './components/WeatherInfo.vue';

export default {
    components:{
        Search,
        WeatherInfo
    },
    data(){
        return {
            weather: null
        }
    },
    computed:{
        weatherClass(){
            return {
                'weather-warm': !this.weather || this.weather.temperature > 15,
                'weather-cold': this.weather && this.weather.temperature < 15
            }
        }
    },
    methods: {
        setWeather(weather){
            this.weather = weather;
        }
    }
}
</script>

<style lang="scss">

    *{
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    body{
        font-family: 'Inconsolata', monospace;
    }
    .image-container{
        background-position: bottom;
        background-size: cover;
        background-repeat: no-repeat;
    }
    .weather-warm{
        background-image: url('./assets/images/warm.jpg');
    }
    .weather-cold{
         background-image: url('./assets/images/cold.jpg');
    }
    .main-container{
        min-height: 100vh;
        padding: 1rem;
        background-image: linear-gradient(to bottom, rgba(0,0,0,.25), rgba(0,0,0,.75));
    }
</style>