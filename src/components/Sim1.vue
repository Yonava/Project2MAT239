<template>
    <div class="maindiv">
        <h1>i) A Roll of the Dice</h1>
        <h1 style="font-size: 12pt">How Many Die Shall We Roll?</h1> 
        <input type="text" placeholder="# of Rolls" v-model="prisoners">
        <h1 style="font-size: 12pt">Sum Required for Freedom</h1> 
        <input type="text" placeholder="Required Sum" v-model="requiredsum">
        <br>
        <div v-if="dice.length > 0" class="dice"> 
            <div class="inline" v-for="die in dice" :key="die.id">
                <!-- <p>Die #{{ die.id }} - {{ die.outcome }}</p> -->
                <img v-if="die.outcome === 1" width="25" src="../assets/one.jpg" alt="dice" />
                <img v-if="die.outcome === 2" width="25" src="../assets/two.jpg" alt="dice" />
                <img v-if="die.outcome === 3" width="25" src="../assets/three.jpg" alt="dice" />
                <img v-if="die.outcome === 4" width="25" src="../assets/four.jpg" alt="dice" />
                <img v-if="die.outcome === 5" width="25" src="../assets/five.jpg" alt="dice" />
                <img v-if="die.outcome === 6" width="25" src="../assets/six.jpg" alt="dice" />
            </div>
        </div> 
        <h1>Sum of Rolls:</h1>
        <h1 :style="totalcolor">{{ total }}</h1>
        <p>*{{ requiredsum }}+ Needed to ensure freedom</p>
        <h1>Chance of Escape:</h1>
        <h1>{{ prob.toFixed(5) }}%</h1>
        <button v-on:click="rolldice()">Roll</button>
    </div>
</template>

<script>
export default {
    name: 'Sim1',
    data: function() {
        return {
            prisoners: 4,
            dice: [],
            total: 0,
            totalcolor: 'color: black;',
            prob: 90,
            iterations: 10000,
            requiredsum: 11
        }
    },
    watch: {
        prisoners() {
            this.functionalProb();
        },
        requiredsum() {
            this.functionalProb();
            this.$emit("sum", this.requiredsum)
        }
    },
    methods: {
        rolldice() {
            
            this.numofdice()
            this.total = 0
            for (let i = 0; i < this.dice.length; i++) {
                this.dice[i].outcome = Math.floor(Math.random()*6)+1
                this.total += this.dice[i].outcome
            }

            if (this.total > this.requiredsum-1) {
                this.totalcolor = 'color: lime;'
            }
            else { 
                this.totalcolor = 'color: crimson;'
            }
            
        },
        numofdice() {
            this.prisoners = parseInt(this.prisoners)
            this.dice = []
            for (let i = 0; i < this.prisoners; i++) {
                this.dice.push({outcome: 0, id: i+1})
            }

        },
        probability() { // not used
            if (this.prisoners > 10) {
                this.prob = 100;
                
            }
            else {


                let outcomes = [];
                let increment = 1;
                for (let i = 0; i < 6**this.prisoners; i++) {
                    let entry = []
                    for (let j = 0; j < this.prisoners; j++) {
                        entry.push(increment)
                    }
                    outcomes.push(entry)
                    increment++;
                    if (increment > 6) increment = 1
                }
                if (this.prisoners > 1) {
                    for (let m = 0; m < this.prisoners-1; m++) {
                        let count = 1;
                        for (let i = 0; i < outcomes.length; i++) {
                            outcomes[i][m] = count
                            if (i % 6 === 0) count++;
                            if (count > 6) count = 1;
                        }
                    }
                }
                console.log(outcomes)


                let desired = 0
                for (let i = 0; i < outcomes.length; i++) {
                    let sum = outcomes[i].reduce((partial_sum, a) => partial_sum + a, 0);
                    
                    if (sum > 10) desired++;
                }
                this.prob = (desired/outcomes.length)*100

            }
        },
        functionalProb() {

            this.iterations = parseInt(this.iterations)
            let desired = 0
            this.prob = 0

            if (this.prisoners >= this.requiredsum) this.prob = 100
            else {
                for (let i = 0; i < this.iterations; i++) {
                    
                    let total = [];
                    for (let j = 0; j < this.prisoners; j++) {
                        let roll = Math.floor(Math.random()*6)+1;
                        total.push(roll);
                    }
                    let sum = total.reduce((partial_sum, a) => partial_sum + a, 0);
                    
                    if (sum > this.requiredsum-1) desired++;
                }
                this.prob = (desired/this.iterations)*100
            }
        }
    },
}
</script>

<style scoped>
.maindiv {
    border: black solid 3px;
    border-radius: 0%;
    padding: 2%;
    margin: 2%;
    background-color: white;
    width: 600px;
    display: block;
    /* padding-bottom: 10%; */
    font-family: 'Courier New', Courier, monospace;
}
.dice {
    
    /* width: 400px; */
    margin: 4%;
    padding: 1%;
    /* border: black solid 1px */
}
.inline {
    
    padding: 1%;
    display: inline-block;
}
h1 {
    font-size: 20pt;
}
button {
    background-color: white;
    font-family: 'Courier New', Courier, monospace;
    font-size: 20pt;
}
</style>
