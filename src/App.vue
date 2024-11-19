<script>
import axios from 'axios';
export default{
    data() {
        return{
            city: '',
            error: '',
            info: null
        }
    },
    methods: {
        getWeather() {
            if (this.city.trim().length < 2) {
                this.error = "you need to enter more tham one symbol"
                return false
            }
            this.error = ''
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=f0ca2288b29e75a0156f895f28397729`)
            .then(res => (this.info = res.data))
        }
    },
    computed:{
        showTemp(){
            return 'tempeture: ' + this.info.main.temp
        },
        showFeelsLike(){
            return 'feels like: ' + this.info.main.feels_like
        },
        showMinTemp(){
            return 'min tempeture: ' + this.info.main.temp_min
        },
        showMaxTemp(){
            return 'max tempeture: ' + this.info.main.temp_max
        }

    }
}
</script>

<template>
    <div class="wrapper">
        <h1>Weather app</h1>
        <p>Check weather in {{ city=='' ? 'your city' :city}}</p>
        <input type="text" placeholder="Enter the city" v-model="city">
        <button v-if="city != ''" @click="getWeather()">Get weather</button>
        <button disabled v-else>Enter your city</button>
        <p class="error">{{ error }}</p>
        <div v-if="info != null">
        <p>{{ showTemp }}</p>
        <p>{{ showFeelsLike }}</p>
        <p>{{ showMinTemp }}</p>
        <p>{{ showMaxTemp }}</p>
    </div>о
    </div>
</template>


<style scoped>
    .wrapper {
        width: 900px;
        height: 500px;
        border-radius: 50px;
        background: #1f0f24;
        text-align: center;
        color: #fff;
        padding: 20px;
    }

    .wrapper h1 {
        margin-top: 50px;
    }

    .wrapper p {
        margin-top: 20px;
    }

    .wrapper input {
        margin-top: 30px;
        border: 0;
        border-bottom: 2px solid #110813;
        background: transparent;
        color: #fcfcfc;
        font-size: 14px;
        outline: none;
        padding: 5px 8px;
    }

    .wrapper input:focus {
        border-bottom-color: #6e2d6e;
    }

    .wrapper button {
        background: #e3bc4b;
        color: #fff;
        border-radius: 10px;
        border:2px solid #b99935;
        padding: 10px 15px;
        margin-left: 20px;
        cursor: pointer;
        transition: transform 500ms ease;
}

.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}

.error {
    color: #d03939
}
</style>
