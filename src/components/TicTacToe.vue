<template>
  <div class="game">
    <div class="board">
      <div class="cell" 
           v-for="(value, i) in fields" 
           :id="i" 
           :key="i"
           @click.prevent="setCellValue"
      ><p class="content">{{ value }}</p></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TicTacToe',
  data: () => ({
    fields: [null,null,null,null,null,null,null,null,null],
    isX: true,
    historyX:[],
    historyO:[],
    allowedCombinationsForX: null,
    allowedCombinationsForO: null,
    winCombinations: [[0, 1, 2],
                      [3, 4, 5],
                      [6, 7, 8],
                      [0, 3, 6],
                      [1, 4, 7],
                      [2, 5, 8],
                      [0, 4, 8],
                      [2, 4, 6]]
  }),
  methods: {
    setCellValue(e) {
      if(this.isX) {
        this.fields[e.toElement.id] = "X"
        this.historyX.push(e.toElement.id)
        console.log(parseInt(e.toElement.id))
        this.allowedCombinationsForX = this.allowedCombinationsForX.filter(_ => _.includes(parseInt(e.toElement.id)))

        console.log('1111',this.allowedCombinationsForX)
        
      }else{
        this.fields[e.toElement.id] = "O"
        this.historyO.push(e.toElement.id)
        this.allowedCombinationsForO = this.allowedCombinationsForO.filter(_ => _.includes(parseInt(e.toElement.id)))

      }
      this.isX= !this.isX
    },
    p() {
      
      console.log()
    }   
  },
  mounted() {
    this.allowedCombinationsForX = this.winCombinations
    this.allowedCombinationsForO = this.winCombinations
  }
}
</script>

<style scoped>
  * {
    margin:0;
    padding: 0;
  }
  .board {
    display: grid;
    grid-template-columns: 5rem 5rem 5rem;
    grid-template-rows: 5rem 5rem 5rem;
  }
  .cell {
    border: 1px solid #bbb;
    text-align: center;
    padding: 10%;
    font-size: 46px;
  }
  .content {
    padding-top: 0.3rem;
  }
</style>
