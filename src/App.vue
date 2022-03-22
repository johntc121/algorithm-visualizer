<template>
  <div>
    <!-- <Navbar @fillArray="fillArray" @bubbleSort="bubbleSort"/> -->
    <div>
        <h1>Sorting Alogrithm Visualizer</h1>
        
        <!-- <select v-model="selectedAlgorithm">
          <option value="bubbleSort">Bubble Sort</option>
          <option>Merge Sort</option>
          <option>Insertion Sort</option>
        </select> -->
        <button @click='bubbleSort'>{{ selectedAlgorithm }}</button>
        <button @click='fillArray'>Shuffle</button>
        <input @change='fillArray' type="range" id="size" name="size"
         min="0" max="50" v-model="size" step="5">
        <label for="size">Size</label>
        <label for="speed">Fast Speed</label>
        <input type="range" id="speed" name="speed"
         min="5" max="500" v-model="speed" step="5">
        <label for="speed">Slow Speed</label>
    </div>

    <div class="container">
      <div ref="bar" class="bar" v-for="(number, index) in array" :key="index" :style="{height: number + 'px'}"></div>
    </div>
  </div>
</template>

<script>
  // import Navbar from './components/Navbar.vue'
  export default {
    name: 'App',
    data() {
      return {
        selectedAlgorithm: 'Bubble Sort',
        array: [],
        size: 5,
        speed: 500,
        sorted: false
      }
    },
    components: {
      // Navbar
    },
    methods: {
      // sortAlgorithm() {
      //   if(selected === 'bubblesort') {
      //     bubbleSort();
      //   })
      // },
      fillArray() {
        this.sorted = false;
        this.array = [];
        for (let i = 0; i < this.size; i++){
          this.array.push(this.getRandomInt(5, 750));
        }
        for (let i = 0; i < this.array.length; i++){
              this.$refs.bar[i].style.backgroundColor = "black";
        }
      },

      getRandomInt(min, max){
        return Math.floor(Math.random() * (max - min + 1)) + min;
      },

      async bubbleSort() {
        if(this.array.length < 1 || this.sorted) {
          return;
        }

        let len = this.array.length;
        let lastUnsortedPosition = len - 1;
        do {
          for(let i = 0; i < len - 1; i++){
            let temp = this.array[i];
            if(this.array[i] > this.array[i + 1]){
              this.$refs.bar[i].style.backgroundColor = "red";
              this.$refs.bar[i+1].style.backgroundColor = "red";
              this.array[i] = this.array[i+1];
              this.array[i+1] = temp;
              await this.sleep();
              this.$refs.bar[i].style.backgroundColor = "black";
              this.$refs.bar[i+1].style.backgroundColor = "black";
              await this.sleep();
            }

            if (temp == (this.array[lastUnsortedPosition])){
              this.$refs.bar[lastUnsortedPosition].style.backgroundColor = "green";
              lastUnsortedPosition--;
            }
          }
        } while(lastUnsortedPosition != 0);
        this.$refs.bar[0].style.backgroundColor = "green";
        this.sorted = true;
      },

      //quicksort
      //merge sort
      //insertion sort
      //selection sort
      //heap sort

      sleep () {
        return new Promise ((resolve) => setTimeout(resolve,this.speed ));
      },
    }
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .container {
    position: fixed;
    left: 100px;
  }

  .bar {
    width: 20px;
    background-color: black;
    display: inline-block;
    margin: 0 5px;
  }
  
  .sorted {
    background-color: green;
  }
  .active {
    background-color: blue;
  }

  #reversedRange {
    direction: rtl
}
</style>
