<template>
    <div v-if="weather">
        <div class="weather-container">
            <div class="location-info">
                <div class="location">{{location}}</div>
                <div class="date">{{weather.date}}</div>
            </div>
            <div class="weather-info">
                <div class="temperature">{{weather.temperature}}°c</div>
                <div class="weather-type">{{weather.weather}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['weather'],
    computed: {
        location(){
            return `${this.weather.place}, ${this.weather.country}`;
        }
    }
}
</script>

<style lang="scss" scoped>
    .weather-container{
        margin-top: 5rem;
    }
    .location-info{
        .location{
            color: $main-color;
            font-size: 2rem;
            font-weight: 800;
            text-align: center;
            text-shadow: 1px 3px rgba(0,0,0,0.25);
            padding-bottom: 10px;;
        }
        .date{
            color: $main-color;
            font-size: 1.2rem;
            font-weight: 400;
            font-style: italic;
            text-align: center;
        }
    }
    .weather-info{
        text-align: center;
        .temperature{
            display: inline-block;
            padding: 10px 25px;
            color: $main-color;
            font-size: 5rem;
            font-weight: 900;
            text-shadow: 3px 6px rgba(0,0,0,0.25);
            background-color: rgba(255,255,255,0.25);
            border-radius: 1rem;
            margin: 1.5rem;
            box-shadow: 3px 6px 10px rgba(0,0,0,0.25);
        }
        .weather-type{
            font-size: 3rem;
            color: $main-color;
            font-weight: 600;
            font-style: italic;
            text-shadow: 3px 3px rgba(0,0,0,0.25);
        }
    }
</style>