<script >
import axios from 'axios'

export default {
    data() {
        return {
            title: {
                ru: 'Погодное приложение',
                en: 'Weather App'
            },
            btn1: {
                ru: 'Получить погоду',
                en: 'Get the weather'
            },
            btn0: {
                ru: 'Введите название города',
                en: 'Write name is city'
            },
            city: '',
            errorru: '',
            erroren: '',
            info: null,
            lang: false,

        }
        // 7b6ac37f932df817f9437f380eb15979  бу айди
    },
    computed: {
        cityName() {
            return this.city
        },
        showTemp() {
            return "Температура:  " + this.info.main.temp
        },
        showFL() {
            return "Ощущается как:  " + this.info.main.feels_like
        },
        showMT() {
            return "Минимальная температура:  " + this.info.main.temp_min
        },
        showMaxT() {
            return "Максимальная температура:  " + this.info.main.temp_max
        },
        showTempEN() {
            return "Temperature:  " + this.info.main.temp
        },
        showFLEN() {
            return "Feels like:  " + this.info.main.feels_like
        },
        showMTEN() {
            return "Minimum temperature:  " + this.info.main.temp_min
        },
        showMaxTEN() {
            return "Maximum temperature:  " + this.info.main.temp_max
        },

    },

    methods: {
        getWeather() {
            if (this.city.trim().length < 2) {
                this.errorru = 'Нужно название более одного символа :)'
                this.erroren = 'Need the name of more than one character :)'
                return false
            }
            this.error = ''
          
            axios.get(`http://api.openweathermap.org/data/2.5/weather?q=${this.city}&lang=ru&units=metric&appid=7b6ac37f932df817f9437f380eb15979`)
                .then(res => (this.info = res.data))
           
          

        },


        langControl() {
            let cl = document.querySelector('.circ')
            if (this.lang == false) {
                cl.style.transform = 'translateX(+30px)'
                this.lang = true
            } else {
                cl.style.transform = 'translateX(0px)'
                this.lang = false
            }
        }
    }
}
</script>
<template>

    <div class="wrapper">
        <div class="language"> RU <div @click="langControl()" class="control">
                <div class="circ"></div>
            </div> EN </div>
        <h1>{{ lang== false ? title.ru : title.en }}</h1>
        <p v-show="lang == false">Узнать погоду в {{ city == "" ? "вашем городе" : city}}</p>
        <p v-show="lang == true">Check the weather in {{ city == "" ? "your city" : city}}</p>
        <input type="text" v-show="lang == false" v-model="city" placeholder="Введите город">
        <input type="text" v-show="lang == true" v-model="city" placeholder="City">
        <button v-if="city != ''" @click="getWeather()">{{ lang== false ? btn1.ru : btn1.en }}</button>
        <button disabled v-else="city != ''">{{ lang== false ? btn0.ru : btn0.en }}</button>
        <p class="error">{{ lang== false ? errorru : erroren }}</p>

        <div v-show="lang == false" v-if="info != null">

            <p>{{ showTemp }}</p>
            <p>{{ showFL }}</p>
            <p>{{ showMT }}</p>
            <p>{{ showMaxT }}</p>
        </div>
        <div v-show="lang == true" v-if="info != null">
            <p>{{ showTempEN }}</p>
            <p>{{ showFLEN }}</p>
            <p>{{ showMTEN }}</p>
            <p>{{ showMaxTEN }}</p>
        </div>
        <footer class="mt-5 text-center text-white">
            <!-- Grid container -->
            <div class="container p-4 pb-0">
              <!-- Section: Social media -->
              <section class="mb-1">
                
                <!-- Twitter -->
                <a class="btn btn-outline-light btn-floating m-1" href="https://t.me/mansur_tg" role="button"
                  ><i class="fab fa-telegram"></i
                ></a>
          
                <!-- Instagram -->
                <a class="btn btn-outline-light btn-floating m-1" href="https://instagram/mansur.fayziev_005?igshid=ZDdkNTZiNTM=" role="button"
                  ><i class="fab fa-instagram"></i
                ></a>
          
                <!-- Linkedin -->
                <a class="btn btn-outline-light btn-floating m-1" href="https://www.linkedin.com/in/%D0%BC%D0%B0%D0%BD%D1%81%D1%83%D1%80-%D1%84%D0%B0%D0%B9%D0%B7%D0%B8%D0%B5%D0%B2-42412425b" role="button"
                  ><i class="fab fa-linkedin-in"></i
                ></a>
          
                <!-- Github -->
                <a class="btn btn-outline-light btn-floating m-1" href="https://github.com/mansurfayziev" role="button"
                  ><i class="fab fa-github"></i
                ></a>
              </section>
              <!-- Section: Social media -->
            </div>
            <!-- Grid container -->
          
            <!-- Copyright -->
            <div class="text-center">
                <span v-show="lang == false">Автор: <a href="" class="link text-white">Мансур Файзиев</a></span>
                <span v-show="lang == true">Author: <a href="" class="link text-white">Mansur Fayziev</a></span>
            </div>

            <!-- Copyright -->
          </footer>
    </div>

</template>
<style scoped>
.language {
    position: relative;
    transform: translate(+80%,10px);
    display: flex;
    align-items: center;

}

.control {
    margin: 0 5px;
    display: flex;
    width: 50px;
    height: 20px;
    background-color: rgb(190, 182, 182);
    border-radius: 50px;
}

.control:hover {
    background-color: #fff;
}

.control .circ {
    background: #000;
    border-radius: 50%;
    height: 20px;
    width: 20px;
    transition: transform 700ms ease;
}

.error {
    color: #d03933;
    ;

}

.wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    background-color: #1f0f24;
    padding: 20px;
    padding-bottom: 0px;
    color: #fff;
    text-align: center;
    transition: transform 1s ease;


}

.wrapper:hover {
    transform: scale(1) translateY(-10px);
}

.wrapper h1 {
    margin-top: 50px;
}

.wrapper p {
    margin-top: 22px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
}

.wrapper input:focus {
    border-bottom-color: #6e2d7d;
}

.wrapper button:disabled {
    background-color: #7b6628;
    cursor: not-allowed;
}

.wrapper button {
    background-color: #e3bc4b;
    color: #fff;
    border-radius: 10px;
    border: 2px solid #b99935;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 500ms ease;

}

.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}
</style>
