<template>
<div id="my_div">
    <h1>Saludos, {{message}}</h1>
    <span v-for="imagen in imagenes" :key="imagen">
        <img :src="imagen" alt="sin imagen">
    </span>
    <button @click="ejemploInterval">Comenzar</button>
    <button @click="stopInterval">Terminar</button>
</div>
</template>

<script>
let intervalTime;
export default {
    name: "HelloVue",
    data() {
        return {
            message: "Segundo comp",
            imagenes: [
                "http://lorempixel.com/300/200/sports",
                "http://lorempixel.com/300/200/nature",
                "http://lorempixel.com/300/200/cats",
                "http://lorempixel.com/300/200/food",
            ],

        };
    },
    methods: {
        ejemploInterval() {
            intervalTime = setInterval(() => {
                const now = Date.now(); //retorna tiempo
                console.log(now);
            }, 1000);
        },
        stopInterval() {
            clearInterval(intervalTime);
        }
    }
};
</script>

<style scoped>
#my_div {
    border: 1px solid red;

    span {
        background: blue;
    }
}
</style>
