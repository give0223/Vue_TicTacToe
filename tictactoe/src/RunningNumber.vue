<template>
  <div>
    <h2 :class="{Running: visibleNumber !== number}">{{visibleNumber}}</h2>
  </div>
</template>


<script>
  export default {
    props:['number'],
    data(){
      return {
        visibleNumber: this.number,
      };
    },
    methods:{
      run(){
        // this.visibleNumber = this.number;
        const diff = Math.floor((this.number - this.visibleNumber) * 0.15);
        if(diff === 0) {
          this.visibleNumber = this.number;
        }else {  
          this.visibleNumber += diff;
          window.requestAnimationFrame(this.run);
          // setTimeout(this.run, 7.8);
        }
      },
    },
    watch:{
      number(){
        this.run();
      },
    }
  };
</script>

<style>
  h2{
    display: inline-block;
    transition: transform 0.15s;
  }
  h2.Running{
    transform: scale(1.3);
    color: green;
  }
</style>
