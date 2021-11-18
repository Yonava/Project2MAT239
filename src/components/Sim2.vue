<template>
<div class="maindiv">
    <center>
        <h1 style="font-size: 12pt">Chance Prisoner Will Flip Coin</h1>
        <div class="sidediv">
            <p>{{ probIn }}%</p>
            <label for="probIn">0%</label>
            <input class="slider" type="range" min="0" max="100" id="probIn" v-model="probIn">
            <label for="probIn">100%</label>
        </div>
    <input type="text" placeholder="Iterations" v-model="iterations">
    <h1>Chance of Escape:</h1>
    <h1>{{ probOut }}%</h1>
    <button v-on:click="simulate">Simulate</button>
    </center>

</div>

</template>

<script>
export default {
    name: 'Sim2',
    data: function() {
        return {
            probIn: 50,
            probOut: 2.0,
            prisoners: 4,
            iterations: '100',
        }
    },
    methods: {

       
        simulate() {
            
            this.probIn = parseInt(this.probIn);
            this.iterations = parseInt(this.iterations)
            this.probOut = 0.0;
            this.probOut = parseFloat(this.probOut)
          
            for (let i = 0; i < this.iterations; i++) {
                let totalFlips = 0;
                for (let j = 0; j < this.prisoners; j++) {
                    let flip = Math.floor(Math.random()*100);
                    flip >= this.probIn ? flip = false:flip = true;
                    if (flip) totalFlips++;
                }
            console.log(this.probOut)
            
                switch (totalFlips) {                  
                    case 1:
                        this.probOut = parseFloat(0.5) + parseFloat(this.probOut);
                        break;
                    case 2:
                        this.probOut = parseFloat(0.25) + parseFloat(this.probOut);
                        break;
                    case 3:
                        this.probOut = parseFloat(0.125) + parseFloat(this.probOut);
                        break;
                    case 4:
                        this.probOut = parseFloat(0.0625) + parseFloat(this.probOut);
                        break;
                    }

            console.log(this.probOut)
            this.probOut = (this.probOut / this.iterations)*100

       
        

            }

        },
        
    }
}
</script>

<style scoped>
input {
    color: black;
    margin: 4%;
}
.slider {
    color: black;
}
.maindiv {
    border: black solid 3px;
    border-radius: 3%;
    padding: 9%;
    margin: 5%;
    width: 15%;
    padding-bottom: 20%;
}
.sidediv {
    border: black solid 2px;
    border-radius: 3%;
    width: 150%;
   
}
h1 {
    font-size: 20pt;
}

</style>
