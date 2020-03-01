<template>
  <div class="home">
    <h1>Statistics Translator</h1>
    
    <!--From section with 2 options-->
    <div class="topSection">
      <div>
        <h3>From</h3>
        
        <!--Option 1: input by time-->
        <div>
          <div class="inputSection">
            <input type="number" min="0" placeholder="hh" v-model.number="fromTimeValue.hours"><span>Hours</span>
          </div>
          <div class="inputSection">
            <input type="number" min="0" placeholder="mm" v-model.number="fromTimeValue.minutes"><span>Minutes</span>
          </div>
          <div class="inputSection">
            <input type="number" min="0" placeholder="ss" v-model.number="fromTimeValue.seconds"><span>Seconds</span>
          </div>
        </div>
        
        <p> -OR- </p>
        
        <!--Option 2: input by number of times doing an activity-->
        <div>
          <div class="inputSection">
            <input type="number" min="0" placeholder="xTimes" v-model.number="fromTimesSpent"><span>Number of times:</span>
          </div>
          <select v-model="fromActivity">
            <option disabled :value="{}">Please select one</option>
            <option v-for="(option, index) in activityOptions" :value="option" :key="index">{{option.action}}</option>
          </select>
        </div>
      </div>
      
      <font-awesome-icon icon="arrow-right" size="3x" color="#42b983"/>
      
      <!--To section-->
      <div>
        <h3>To</h3>
        <span>Average number of times:</span>
        <select v-model="toActivity">
          <option disabled :value="{}">Please select one</option>
          <option v-for="(option, index) in activityOptions" :value="option" :key="index">{{option.action}}</option>
        </select>
      </div>
    </div>
    
    <!--Button section-->
    <button type="button" @click="calculate" :disabled="!toActivity.hasOwnProperty('action')"> Calculate </button>
    <button type="button" @click="reset"> Reset </button>
    
    <!--Results section-->
    <div v-if="resultsShown" class="resultsBox">
      <hr>
      <h3>Results</h3>
      <p>{{funnyExclamation}}</p>
      <p>In 
        <span class="specialText">{{this.fromTimeValue.hours}}</span> hours, 
        <span class="specialText">{{this.fromTimeValue.minutes}}</span> minutes, 
        and 
        <span class="specialText">{{this.fromTimeValue.seconds}}</span> seconds, 
        you could have completed (on average)
        <span class="specialText">"{{toActivity.action}}" {{timeResult}} times</span> 
      </p>
      
      <p> -OR- </p>
    
      <p v-if="fromActivity.action"> 
        In the time spent
        <span class="specialText">"{{fromActivity.action}}" {{fromTimesSpent}} times</span>
        you could have completed (on average)
        <span class="specialText">"{{toActivity.action}}" {{activityResult}} times</span>
      </p> 
      <p v-else>(No from activity given)</p>
    </div>
  </div>
</template>

<style scoped>
  h3 {
    text-decoration: underline;
  }
  
  select {
    padding: 10px 20px;
    width: 100%;
  }
  
  .topSection {
    display: flex; 
    justify-content: space-around; 
    align-items: center;
  }
  
  .specialText {
    color: #42b983;
    font-weight: bold;
    font-size: 25px;
  }
  
  .resultsBox {
    padding: 20px;
  }
</style>

<script>
  export default {
    name: "Home",
    props: {
      activityOptions: Array
    },
    data: function() {
      return {
        resultsShown: false,
        fromTimesSpent: 0,
        fromTimeValue: {
          hours: 0,
          minutes: 0,
          seconds: 0
        },
        toActivity: {},
        fromActivity: {},
        funnyExclamation: "",
        exclamationItems: ["Wow! Thats a lot of time!", "Think about what this means", "Are you proud of yourself?", "Why this is interesting"],
        timeResult: 0,
        activityResult: 0
      }
    },
    methods: {
      reset: function() {
        this.toActivity = {},
        this.fromActivity = {},
        this.fromTimeValue.hours = 0;
        this.fromTimeValue.minutes = 0;
        this.fromTimeValue.seconds = 0;
        this.fromTimesSpent = 0;
        this.resultsShown = false;
      },
      calculate: function() {
        let secondsTotal = (this.fromTimeValue.hours * 60 * 60) + (this.fromTimeValue.minutes * 60) + this.fromTimeValue.seconds;
        this.timeResult = Math.floor((secondsTotal/this.toActivity.secondsAvg) * 1000) / 1000;
        this.activityResult = Math.floor(((this.fromActivity.secondsAvg * this.fromTimesSpent)/this.toActivity.secondsAvg) * 1000) / 1000;
        this.funnyExclamation = this.exclamationItems[Math.floor(Math.random() * this.exclamationItems.length)];
        this.resultsShown = true;
      }
    },
    computed: {

    }
  };
</script>