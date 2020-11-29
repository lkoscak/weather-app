<template>
    <div class="search-box">
        <input 
        type="text" 
        class="search-field" 
        placeholder="Search for a place..." 
        autocomplete="off" 
        autocorrect="off" 
        autocapitalize="off" 
        spellcheck="false"
        v-model="place"
        @keypress.enter="fetchWeather">
    </div>
</template>

<script>
export default {
    data(){
        return {
            place: '',
            apiCallTimer: null
        }
    },
    computed: {
        apiCallUrl(){
            return `http://api.openweathermap.org/data/2.5/weather?q=${this.place}&units=metric&appid=${process.env.VUE_APP_WEATHER_API}`;
        }
    },
    watch:{
        place(){
            clearTimeout(this.apiCallTimer);
            this.apiCallTimer = setTimeout(() => {
                this.requestWeather();
            }, 2000);
        }
    },
    methods: {
        fetchWeather(){
            clearTimeout(this.apiCallTimer);
            this.requestWeather();
        },
        async requestWeather(){
            if(this.place === "") return;
            let result = await fetch(this.apiCallUrl);
            let data = await result.json();
            if(data.name === undefined) return;
            let weather = this.createWeatherObject(data);
            this.$emit('set-weather', weather);
        },
        createWeatherObject(data){
            return {
                place: data.name,
                country: data.sys.country,
                date: this.buildDate(),
                temperature: Math.round(data.main.temp),
                weather: data.weather[0].main
            }
        },
        buildDate(){
            let today = new Date();
            let months = ["January", "February", "March", "April",
            "May", "June", "July", "August", "September", "October",
            "November", "December"];
            let weekDays = ["Monday", "Tuesday", "Wednesday", "Thursday",
            "Friday", "Saturday", "Sunday"];
            return `${weekDays[today.getDay()]} ${today.getDate()}. ${months[today.getMonth()]} ${today.getFullYear()}`;
        }
    },
    emits: ['set-weather']
}
</script>

<style lang="scss" scoped>
    .search-box {
        margin-top: 3rem;
        .search-field{
            display: block;
            width: 100%;
            padding: 1rem;
            font-size: 1.1rem;
            color: $main-text-color;

            appearance: none;
            border: none;
            background: none;
            outline: none;
            background-color: rgba(186, 232, 232, 0.45);
            border-radius: 20px 0 20px 0;
            box-shadow: 0px 0px 10px rgba(0,0,0,.35);

            transition: 
            background-color .5s ease-in,
            border-radius .5s ease-in;

            &:focus{
                background-color: rgba(186, 232, 232, 0.7);
                border-radius: 0 20px 0 20px;
            }
        }
        ::placeholder{
            color: $main-text-color;
            opacity: .7;
        }
    }
</style>