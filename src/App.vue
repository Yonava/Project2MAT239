<template>
    <div>
      <center>
        <div class="title">
        <h1 style="font-family: 'Courier New', Courier, monospace;">MAT239 Project II, Yona Voss-Andreae</h1>
        </div>
        <div class="maindiv">
          <Sim1 ref="sim1" />
          <Sim2 />
          <Sim3 />
        </div>
      </center>
      <div class="essay">
        <h1>Abstract:</h1>
      <p>
        The prisoner's dilemma is a classic in the study of game theory.
        The most famous scenario is elaborated using the following example.
        Two partners in crime have been arrested by police and are brought in for
        interrogation. The detectives, looking to seal a conviction, hatch a plan they
        believe will get them closer to cracking the case. The two arrested subjects are escorted
        into separate rooms without the ability to communicate with one another. Next,
        the detectives lay out a proposition to each of them. The detectives tell both of them
        that they have precisely two options. The first option: cooperate with the investigation
        by snitching on your partner, if your partner chooses to remain quiet and not snitch on
        you, you go free and your partner gets 3 years behind bars. The second option: Remain quiet.
        However, if your partner snitches, you end up being the one serving 3 years.
        Alternatively if you both stay quiet you get 1 year each, if both of you talk,
        you are each looking at 2 years in jail. What will you do? Staying quiet, while
        risking the possibility of the maximum sentence is the best decision from the group's standpoint,
        while cooperating with investigators could land you and your partner in jail
        a combined 4 years, twice as long. 
        In Discrete Mathematics, Project II, the dilemma our prisoners are given follow circumstances
        in which simulating probability can determine with near certainty what the best chances of
        escape are for our prisoners encountered in each scenario. Read the following three scenario
        descriptions. I encourage you to experiment with the numbers attached to each simulation to see how
        close to freedom you can get our prisoners.
      </p>
      <h1>i)</h1>
      <p>
        This scenario presents itself pretty straightforwardly, each prisoner is given a choice
        to roll a fair, six sided die. For the prisoners to be set free, they need to require 
        that the dice rolled show a minimum sum of eleven. The strategy is clear, the more dice that are 
        rolled, the better the odds of escape. The odds shown are a simulation that is expressed with 
        the following pseudo code:
      </p>
      <img class="example" src="./assets/example1.jpg" alt="example1">
      </div>
    </div>
</template>

<script>

import Sim1 from './components/Sim1.vue'
import Sim2 from './components/Sim2.vue'
import Sim3 from './components/Sim3.vue'

export default {
  name: 'App',
  components: {
    Sim1,
    Sim2,
    Sim3
  },
  mounted() {
    this.$refs.sim1.rolldice()
    this.$refs.sim1.functionalProb()
  }
}
</script>

<style>
.maindiv {
    border: black solid 3px;
    /* border-radius: 1%; */
    background-color: lightblue;
    display: inline-flex;
    /* padding-bottom: 10%; */
    font-family: 'Courier New', Courier, monospace;
    margin: 2px;
}
.essay {
  font-family: 'Courier New', Courier, monospace;
  border: black solid 3px;
  font-size: 18pt;
  padding: 2%;
  margin: 2%;
  background-color: rgb(247, 210, 195);
}
.title {
  border: black solid 3px;
  /* position: sticky; */
  /* top: 0; */
  background: rgb(180, 238, 87);
  width: 900px;
  margin: 2%
}
.example {
  border: black solid 3px;
  
}
</style>
