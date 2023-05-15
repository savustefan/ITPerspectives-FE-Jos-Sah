
<template>

    <div class="tabla-text-stanga">
        <p class="text-stanga">8</p>
        <p class="text-stanga">7</p>
        <p class="text-stanga">6</p>
        <p class="text-stanga">5</p>
        <p class="text-stanga">4</p>
        <p class="text-stanga">3</p>
        <p class="text-stanga">2</p>
        <p class="text-stanga">1</p>
    </div>

    <div class="tabla">

        <div v-for="col in 8" :key="col" class="tabla-coloana">
            <div v-for="row in 8" :key="row" class="tabla-patrat" :class="[(col + row) % 2 === 0 ? 'alb' : 'negru']">

                <!--Piese negre-->
                <div v-if="col === 1 && row === pozitiePion">&#9823;</div>
                <div v-if="col === 2 && row === 2">&#9823;</div>
                <div v-if="col === 3 && row === 2">&#9823;</div>
                <div v-if="col === 4 && row === 2">&#9823;</div>
                <div v-if="col === 5 && row === 2">&#9823;</div>
                <div v-if="col === 6 && row === 2">&#9823;</div>
                <div v-if="col === 7 && row === 2">&#9823;</div>
                <div v-if="col === 8 && row === 2">&#9823;</div>

                <div v-if="col === 1 && row === 1">&#9820;</div>
                <div v-if="col === 2 && row === 1">&#9822;</div>
                <div v-if="col === colNebun && row === randNebun">&#9821;</div>
                <div v-if="col === 4 && row === 1">&#9818;</div>
                <div v-if="col === 5 && row === 1">&#9819;</div>
                <div v-if="col === 6 && row === 1">&#9821;</div>
                <div v-if="col === 7 && row === 1">&#9822;</div>
                <div v-if="col === 8 && row === 1">&#9820;</div>

                <!--Piese albe-->
                <div v-if="col === 1 && row === 7">&#9817;</div>
                <div v-if="col === 2 && row === 7">&#9817;</div>
                <div v-if="col === 3 && row === 7">&#9817;</div>
                <div v-if="col === 4 && row === 7">&#9817;</div>
                <div v-if="col === 5 && row === 7">&#9817;</div>
                <div v-if="col === 6 && row === 7">&#9817;</div>
                <div v-if="col === 7 && row === 7">&#9817;</div>
                <div v-if="col === 8 && row === 7">&#9817;</div>

                <div v-if="col === 1 && row === 8">&#9814;</div>
                <div v-if="col === 2 && row === 8">&#9816;</div>
                <div v-if="col === 3 && row === 8">&#9815;</div>
                <div v-if="col === 4 && row === 8">&#9815;</div>
                <div v-if="col === 5 && row === 8">&#9813;</div>
                <div v-if="col === 6 && row === 8">&#9812;</div>
                <div v-if="col === 7 && row === 8">&#9816;</div>
                <div v-if="col === 8 && row === 8">&#9814;</div>

            </div>

        </div>
        <p class="tabla-text-jos">A</p>
        <p class="tabla-text-jos">B</p>
        <p class="tabla-text-jos">C</p>
        <p class="tabla-text-jos">D</p>
        <p class="tabla-text-jos">E</p>
        <p class="tabla-text-jos">F</p>
        <p class="tabla-text-jos">G</p>
        <p class="tabla-text-jos">H</p>
    </div>

    <div class="container-btn">

        <button class="btn" @click="mutaPion(), coundownTimer()">Mută Pion</button>
        <button class="btn" @click="mutaNebun()">Mută Nebun</button>
        <p class="p-timer">Timp rămas: {{ timer }}</p>

    </div>

</template>


<script>

export default {

    data() {
        return {
            colNebun: 3,
            randNebun: 1,
            pozitiePion: 2,
            timer: 10,
        };
    },

    methods: {

        mutaNebun() {
            if (this.colNebun < 8 && this.randNebun < 8) {
                this.randNebun += 1;
                this.colNebun += 1;
            } else if (this.colNebun < 8 && this.randNebun === 8) {
                this.randNebun -= 1;
                this.colNebun += 1;
            } else if (this.colNebun === 8 && this.randNebun === 8) {
                this.randNebun = this.randNebun - 3;
                this.colNebun = 1;
            } else if (this.colNebun === 8 && this.randNebun < 8) {
                this.randNebun += 1;
                this.colNebun -= 1;
            }
        },

        mutaPion() {

            if (this.pozitiePion < 8) {
                const audio = new Audio('/src/assets/chess_sound.mp3')
                audio.play();
                setTimeout(()=>{
                    this.pozitiePion += 1;
                    this.timer = 10;
                }, 250);


            } else {
                alert("Șah mat!");
            }

        },

        coundownTimer(){

            if (this.timer > 0){
                setTimeout(()=> {
                    this.timer -=1;
                    this.coundownTimer()
                }, 1000);
            } else if (this.timer === 0){
                this.timer = 10;
            }

        }

    },

};

</script>
