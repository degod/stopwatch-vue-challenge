<template>
  <div class="hello">
    <h1>Stopwatch</h1>

    <b>{{ timer }}</b><br>

    <button @click="toggleTimer">{{ timerBtn }}</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: ()=>({
    timer: '00:00:00',  // For displaying the timer
    timerBtn: 'Start',  // For the button label
    timeCount: 0,       // To hold the timer count in hundredths
    toggler: false,     // To keep track of the timer button toggle
    timeFunc: null      // A function to hold the timer interval - to set/clear easily
  }),
  methods: {
    toggleTimer(){
      if(this.toggler == false){
        this.startTimer();  // Execute the start function when toggler has not been pressed/stopped
      }else{
        this.stopTimer();   // Execute the stop function when toggler is not false
      }
      this.toggler = !this.toggler; // Toggle variable to indicate that button is pressed
    },
    startTimer(){
      let minutes = 0;    // A variable to hold the minutes of the time
      let seconds = 0;    // A variable to hold the seconds of the time
      let hundredths = 0; // A variable to hold the hundredths of the time

      // CREATE A SET-INTERVAL FOR TIMER FOR EVERY 10 MILLISECONDS
      this.timeFunc = setInterval(()=>{
        this.timeCount++; // Increment the timer count every 10 milliseconds

        // RETURN THE timeCount VARIABLE / THE MODULUS BY 99 FOR HUNDREDTHS
        hundredths = (this.timeCount == 100) ? 0 : (      // Return 0 if hundredths equals to 100
            (this.timeCount > 100) ? this.timeCount%100: this.timeCount
        );

        // RETURN THE DIVISION BY 100 OF THE timeCount VARIABLE FOR SECONDS
        seconds = (this.timeCount>100) ? Math.floor(this.timeCount/100): 0;
        seconds = (seconds == 60) ? 0 : (                 // Return 0 if seconds equals to 60
            (seconds > 60) ? seconds%60 : seconds         // Return modulus of 59 if seconds goes beyond 59
        );  

        // RETURN THE DIVISION BY 6000 OF THE timeCount VARIABLE FOR MINUTES
        minutes = (this.timeCount>6000) ? Math.floor(this.timeCount/6000): 0;

        // MAKE ALL VARIABLES SHOW IN DOUBLE DIGITS
        var hundredthsLabel = (hundredths < 10) ? '0'+hundredths: hundredths; // For hundredths
        var secondsLabel = (seconds < 10) ? '0'+seconds: seconds;             // For seconds
        var minutesLabel = (minutes < 10) ? '0'+minutes: minutes;             // For minutes

        // CONCATENATE minutesLabel, secondsLabel AND hundredthsLabel FOR DISPLAY
        this.timer = minutesLabel + ":" + secondsLabel + ":" + hundredthsLabel;
      }, 10);

      this.timerBtn = 'Stop'; // Change the label of the trigger button to "Stop"
    },
    stopTimer(){
      clearInterval(this.timeFunc); // Clear the running interval
      this.timeCount = 0;           // Reset the timer count to "0"
      this.timer = '00:00:00';      // Reset the timer display to default
      this.timerBtn = 'Start';      // Change the label of the trigger button to "Stop"
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  b {
    font-size: 80px;
    color: #42b983;
  }
  button {
    display: inline-block;
    width: 180px;
    height: 55px;
    font-size: 22px;
    margin-top: 30px;
    cursor: pointer;
    background-color: #000;
    color: #fff;
    border-radius: 5px;
    border: none;
  }
</style>





