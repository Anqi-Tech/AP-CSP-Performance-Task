<template>
    <div>
        <div v-for="die in dice" :key="die.id" class="dice" @click="selectDice">
            <p>{{die.number}}</p>
        </div>
        <h1 @click="selectSkill1">Deal [number] x 10 damage</h1>
        <h1 @click="selectSkill2">Heal [number] x 5 health</h1>
    </div>
</template>

<script>
export default {
   data() {
    return {
      dice: [],
      diceSelected: false,
      skillSelected: false,
      diceNumber: null,
      damageNumber: null,
      healNumber: null,
    }
  },
  methods: {
    selectDice(e) {
        const targetDice = e.target
        this.diceNumber = targetDice.innerText
        this.diceSelected = true
        console.log(this.diceNumber)
    },
    selectSkill1() {
      if (this.diceSelected == true) {
        this.damageNumber = this.diceNumber * 10
        console.log(this.damageNumber)
      }
    }
  },
  mounted() {
    for (let i = 0; i < 4; i++) {
    let randomNumber = Math.floor(Math.random()*6)+1
    this.dice.push({number: randomNumber})
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