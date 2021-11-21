<template>
    <div>
      <a id="simulators"></a>
      <center>
        <div class="title">
        <h1 style="font-family: 'Courier New', Courier, monospace;">MAT239 Project II, Yona Voss-Andreae</h1>
        </div>
        <div class="maindiv">
          <Sim1 ref="sim1" @sum="updatesum($event)"/>
          <Sim2 />
          <Sim3 />
        </div>
      
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
        risking the possibility of the maximum sentence is the best decision from the groups standpoint,
        while cooperating with investigators could land you and your partner in jail
        a combined 4 years, twice as long. 
        In Discrete Mathematics, Project II, the dilemma our prisoners are given follow circumstances
        in which simulating probability can determine, within an order of approximation, what the likelihood of
        escape is. Read the following three scenario
        descriptions. I encourage you to experiment with the numbers attached to each simulation to see how
        close to freedom you can get our prisoners.
      </p>
      <h1>i)</h1>
      <p>
        This scenario presents itself pretty straightforwardly, each prisoner is given a choice
        to roll a fair, six sided die. For the prisoners to be set free, the dice need to show a minimum sum
        of {{ requiredSum }}. 
        The strategy is clear, the more dice that are 
        rolled, the better the odds of escape. The odds shown are a simulation that is expressed with 
        the following pseudo code:
      </p>
      <img class="example" src="./assets/example1.jpg" alt="example1">
      <h1>ii)</h1>
      <p>
        In scenario 2, the prisoners are isolated into separate cells and given a choice to flip a coin. 
        If all the coins flipped come up tails, the prisoners are released. However, if any coin 
        flipped by any of the prisoners lands on heads, no one is freed. Furthermore, if no coins get 
        flipped, everyone remains locked up. While this question would be an interesting game from a psychological 
        standpoint, one more tool is given to each prisoner. This tool is a random number generator, calibrated with 
        the slider, that informs each prisoner individually whether to flip the coin or not. In the case of 4 
        prisoners, informing the prisoners to flip approximately 34% of the time is optimal. To understand why, we 
        must go over the probability of escape given n number of times the coin is flipped:
      </p>
      <img class="example" src="./assets/equation1.jpg" alt="equation1">
      <p>
        If we map n to the probability of escape we get:
        (0, 0), (1, .5), (2, .25), (3, .125), (4, .0625)
      </p>
      <p>
        When attempting to optimize the outcome of escape, what must be noted
        is that the effects of no prisoners flipping is weighted far heavier negatively than if 2 prisoners flip.
        If the prisoners flip 25% of the time, no coins are flipped too often for it to be a tenable solution.
      </p>
      <p>
        Play around with the simulator, increasing iterations will produce a result with higher precision.
        Adjusting prisoners, and the flip probability may yield unexpected or suprising results!
      </p>
      <h1>iii)</h1>
      <p>
        Scenario 3 acts a lot like scenario 2. The difference between them is that while scenario 2 uses a coin flip
        as a determinant in whether the group of inmates gets to walk free, now it's a die. The same rules as the last
        game apply, however, now they must role an odd number instead of tails. When determining the probability
        of a desired outcome, in this case rolling odd numbers on a six sided die, the equation is
        <b># of desired outcomes / all possible outcomes</b>
        or 3/6. Flipping a coin has 2 possible outcomes (heads or tails) which is 1/2. Simplifying 3/6 gives us 1/2,
        due to this, scenairo 2 and 3 both reduce to the same odds. Lets write a simulation for the probability of
        escape given 4 prisoners, played out over 100 games in pseudo code:
      </p>
      <img class="example" src="./assets/example2.jpg" alt="example2">
      <h1>Time to Experiment:</h1>
      <a href="#simulators">
      <h2>Back to Simulations!</h2>
      </a>
      </div>
      </center>
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
  data: function() {
    return {
      requiredSum: 11,
    }
  },
  methods: {
    updatesum(x) {
      this.requiredSum = x
    }
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
