<template>
    <div>
        <h1>Sorting Alogrithm Visualizer</h1>

        <div>Selected: {{ selectedAlgorithm }}</div>

        <select v-model="selectedAlgorithm">
        <option disabled value="">Please select one</option>
        <option>Bubble Sort</option>
        <option>Quick Sort</option>
        <option>Merge Sort</option>
        </select><br />
        <button @click="$emit('bubbleSort')">{{ selectedAlgorithm }}</button>
        <button @click="$emit('fillArray')">Shuffle</button>
        <input type="range" id="size" name="size"
         min="0" max="50" v-model="size" step="5">
        <label for="size">Size</label>
        <input type="range" id="speed" name="speed"
         min="0" max="50" v-model="speed" step="5">
        <label for="speed">Speed</label>
    </div>
</template>

<script>

export default {
    name: 'Navbar',
        data() {
            return {
                selectedAlgorithm: '',
                size: 5,
                speed: 50
            }
        },
    }
</script>

<style>

</style>