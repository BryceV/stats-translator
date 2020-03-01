<template>
  <div id="app">
    <div id="nav">
      <router-link active to="/">Home</router-link> |
      <router-link to="/edit">Edit Listings</router-link>
    </div>
    <hr>
    <router-view :activityOptions="activityOptions" :deleteAction="deleteAction" :addAction="addAction"/>
  </div>
</template>

<script>
  export default {
    name: "App",
    data: function() {
      return {
        activityOptions: [{action: "Run a mile", secondsAvg: 600}, {action: "Fall asleep", secondsAvg: 1200}, 
        {action: "Work days", secondsAvg: 28800}, {action: "Blinked", secondsAvg: 4},
        {action: "Count to a million", secondsAvg: 1000000}, {action: "Count to a billion", secondsAvg: 1000000000},
        {action: "Tying a shoe", secondsAvg: 30}, {action: "Watch an nfl game", secondsAvg: 10800}, 
        {action: "Watch an nba game", secondsAvg: 8400}],
      }
    },
    methods: {
      deleteAction(index) {
        let arrayClone = JSON.parse(JSON.stringify(this.activityOptions));
        arrayClone.splice(index, 1);
        this.activityOptions = arrayClone;
      },
      addAction(name, time) {
        let arrayClone = JSON.parse(JSON.stringify(this.activityOptions));
        arrayClone.unshift({action: name, secondsAvg: time})
        this.activityOptions = arrayClone;
      }
    }
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  #nav {
    padding: 10px;
  }

  #nav a {
    font-weight: bold;
    color: #2c3e50;
  }

  #nav a.router-link-exact-active {
    color: #42b983;
  }
  
  .inputSection {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  input {
    margin: 5px;
    width: 80%
  }
  
  button {
    margin: 10px;
    padding: 10px;
    border: #a9a9a9 solid .1px;
    font-weight: bold;
  }
  
  button:hover {
    background-color: #42b983;
  }
</style>