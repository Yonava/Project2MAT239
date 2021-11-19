<template>
<div class="maindiv">
    <h1>ii) The Coin Flip</h1>
    <center>
        <h1 style="font-size: 12pt">Number of Captives</h1>
        <input type="text" placeholder="# of Prisoners" v-model="prisoners"/>
        <h1 style="font-size: 12pt">Chance Prisoner Will Flip Coin</h1>
        <div class="sidediv">
            <p>{{ probIn }}%</p>
            <label for="probIn">0%</label>
            <input class="slider" type="range" min="0" max="100" id="probIn" v-model="probIn">
            <label for="probIn">100%</label>
        </div>
    <h1 style="font-size: 12pt">Number of Iterations</h1>
    <input type="text" placeholder="Iterations" v-model="iterations">
    <h1>Chance of Escape:</h1>
    <h1>{{ probOut.toFixed(5) }}%</h1>
    <button v-bind:class="simclass" v-on:click="init">{{ simbutton }}</button>
    </center>

</div>

</template>

<script>
export default {
    name: 'Sim2',
    data: function() {
        return {
            probIn: 50,
            probOut: 0,
            prisoners: 4,
            iterations: '100',
            simbutton: 'Simulate',
            simclass: ''
        }
    },
    methods: {

        init() {

            this.simbutton = 'Thinking...'
            this.simclass = 'r'
            setTimeout(this.simulate, 1)


        },
       
        simulate() {
            
            this.prisoners = parseInt(this.prisoners)
            this.probIn = parseInt(this.probIn)
            this.iterations = parseInt(this.iterations)
            
            let result = 0

            for (let i = 0; i < this.iterations; i++) {
                let totalFlips = 0;
                for (let j = 0; j < this.prisoners; j++) {
                    let flip = Math.floor(Math.random()*100);
                    flip >= this.probIn ? flip = false:flip = true;
                    if (flip) totalFlips++;
                }
            
                switch (totalFlips) {                  
                    case 1:
                        result += 0.5;
                        break;
                    case 2:
                        result += 0.25;
                        break;
                    case 3:
                        result += 0.125;
                        break;
                    case 4:
                        result += 0.0625;
                        break;
                }
            }

            this.probOut = (result / this.iterations)*100
            this.simbutton = 'Simulate'
            this.simclass = ''

        },
        
    }
}
</script>

<style scoped>
input {
    color: black;
    /* margin: 4%; */
}
.slider {
    color: black;
}
.maindiv {
    border: black solid 3px;
    border-radius: 0%;
    background-color: white;
    display: block;
    padding: 2%;
    margin: 2%;
    width: 600px;
    /* padding-bottom: 10%; */
    font-family: 'Courier New', Courier, monospace;
}
.sidediv {
    border: black solid 2px;
    
}
h1 {
    font-size: 20pt;
}
button {
    background-color: white;
    font-family: 'Courier New', Courier, monospace;
    font-size: 20pt;
}
.r {
    color:tomato
}


</style>
