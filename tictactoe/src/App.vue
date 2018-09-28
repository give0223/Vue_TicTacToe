<template>
  <div class="app">
    <div class="board">
      <div 
        class="grid" 
        v-for="(grid,idx) in grids" 
        :key="idx" 
        @click="setgrid(idx)"
      >
        {{getSymbol(grid)}}
      </div>
    </div>
    <div>
      <span>Player: {{getSymbol(player)}}</span>
      <br/>
      <span>Winner: {{getSymbol(winner)}}</span>
      <br/>
      <button @click="reset">ResetGame</button>
    </div>
  </div>
</template>

<script>
const Lines = [
  [0,1,2],[3,4,5],[6,7,8],
  [0,3,6],[1,4,7],[2,5,8],
  [0,4,8],[2,4,6],
];
  export default {
    data(){
      return{
        winner: 0,
        player: 1,
        grids:[0,0,0,0,0,0,0,0,0],
      };
    },
    methods:{
      setgrid(idx){
        if(this.grids[idx] !== 0) return;
        if(this.winner !== 0) return;
        this.$set(this.grids, idx, this.player);
        this.player = -this.player;
        this.winner = this.getWinner();
      },
      getSymbol(num){
        return num === 0 ? '' : num === 1 ? 'O' : 'X';
      },
      getWinner(){
        for(let i=0; i < 8; i++){
          const line = Lines[i];
          const [a,b,c] = line;
          const sun = this.grids[a] + this.grids[b] + this.grids[c];
          if(sun === 3) return 1;
          if(sun === -3) return -1;
        }
        return 0;
      },
      reset(){
        this.winner = 0;
        this.player = 1;
        this.grids = [
          0,0,0,
          0,0,0,
          0,0,0
        ];
      },
    },
  };
</script>


<style>
.board{
  display: flex;
  flex-flow: row wrap;
  width: 400px;
  height: 400px;
  align-content: flex-start;
  margin: 30px auto;
}

.grid{
  width: 33%;
  height: 33%;
  border: 1px solid green;
  box-sizing: border-box;
  font-size: 30px;
  text-align: center;
  line-height:130px;
}
</style>