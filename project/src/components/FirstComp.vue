<template>
    <div>
        <div v-for="die in dice" :key="die.id" class="dice" @click="selectDice">
            <p>{{die.number}}</p>
        </div>
        <h1>Insert box here</h1>
    </div>
</template>

<script>
export default {
   data() {
    return {
      dice: [
        {number: '1'},
        {number: '2'},
        {number: '3'},
        {number: '4'},
      ],
      diceSelected: false,
      skillSelected: false,
    }
  },
  methods: {
    selectDice(e) {
        const b = e.target
        console.log(b)
    }
  }
}
</script>

<style scoped>
.dice {
    background: red;
    width: 5vw;
    aspect-ratio: 1 / 1;
    font-size: 2rem;
    text-align: center;
    margin: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
}

p {
    margin: 0;
}

</style>