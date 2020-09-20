<template>
  <div id="app">
      <div class="count">
    <div class="title">
        <h1>{{message}}</h1>
    </div>
    <div class="time">
        {{time}} {{det}}
    </div>
    <div class="buttons">
    <button class="btn" @click="count(3)">3s</button>
    <button class="btn" @click="count(60)">1m</button>
    <button class="btn" @click="count(300)">5m</button>
    <button class="btn" @click="count(600)">10m</button>
    <button class="btn" @click="count(1800)">30m</button>
    </div>
    </div>

  </div>
</template>
</template>

<script>
let interval
  export default {
    name: "countdown",
    data() {
      return {
        message: 'Cuenta Regresiva',
        time:"00:00",
        det: "min/seg"
      };
    },
    methods:{
        count:function(seg){
            //set de hora actual + tiempo de descuento
          clearInterval(interval)
            const now= Date.now()          
            const end= now +seg*1000;
            this.stopInterval(end)
            
        },
        stopInterval:function(end){

            interval=setInterval(()=>{
                //no sé como lo hice, pero funciona. Busque ayuda en la web,
                //pero esta fue la manera en que mejor entendí (esa era la idea, no?)
                const rest = Math.round((end-Date.now())/1000);
                if (rest<0){
                    clearInterval(interval);
                    return;
                }
                const minutes= Math.floor((rest % 3600)/60);
                const seconds= rest % 60;
                console.log(minutes, seconds)
                if ((String(seconds).length)===1 && (String(minutes).length)===1 ){
                    this.time=`0${minutes}:0${seconds}`
                }else if((String(seconds).length)===1 && (String(minutes).length)!=1 ){
                    this.time=`${minutes}:0${seconds}`
                }else if((String(seconds).length)!=1 && (String(minutes).length)===1 ){
                    this.time=`0${minutes}:${seconds}`
                }else{
                this.time=`${minutes}:${seconds}`
                }
                
            },1000)
            
        }
    },
    mounted:function(){
    }
}
</script>

<style scoped>


.count {
    text-align: center;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-template-rows: repeat(5, 1fr);
    grid-column-gap: 10px;
    grid-row-gap: 20px;
    font-family: Arial, Helvetica, sans-serif;
    color: grey;
}

.title {
    grid-area: 1 / 2 / 2 / 5;
}

.time {
    grid-area: 2 / 2 / 3 / 5;
    font-size: 30px;
    font-weight: bolder;
    
}

.buttons {
    grid-area: 3 / 2 / 4 / 5;
}
.btn {
    padding: 10px 20px;
color: white;
background: green;
border: 1px solid greenyellow;
border-radius: 5px;
cursor: pointer;
margin: 0 20px;
font-size: 20px;
}
.btn:hover {
    background: black;
}
</style>
