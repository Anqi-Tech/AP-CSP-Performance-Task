<template>
    <div>
      <div class="game-field">
        <div>
          <h1>Hi: {{playerHealth}}</h1>
        </div>
        <div>
          <h1 @click="selectSkill1">Deal [number] x 10 damage</h1>
          <h1 @click="selectSkill2">Heal [number] x 5 health</h1>
        </div>
        <div>
          <h1>Bye: {{enemyHealth}}</h1>
        </div>
      </div>
      <div class="game-dice">
        <div v-for="(die, index) in dice" :key="die.id" class="dice" @click="selectDice">
            <p>{{die.number}}</p>
            <p class="hide">{{index}}</p>
        </div>
      </div>
    </div>
</template>

<script>
export default {
   data() {
    return {
      dice: [],
      targetedDice: null,
      diceNumber: null,
      indexNumber: null,
      diceSelected: false,
      skillSelected: false,
      damageNumber: null,
      healNumber: null,
      playerHealth: 100,
      enemyHealth: 1000,
    }
  },
  methods: {
    selectDice(e) {
      if (e.target.tagName == 'DIV') {
        this.targetedDice = e.target
      } else {
        this.targetedDice = e.target.parentElement
      }
        this.diceNumber = this.targetedDice.innerText
        this.indexNumber = this.targetedDice.lastElementChild.innerHTML
        this.diceSelected = true
    },
    selectSkill1() {
      if (this.diceSelected == true) {
        const usedDice = this.dice[this.indexNumber]
        this.dice = this.dice.filter((d) => d !== usedDice)
        this.damageNumber = this.diceNumber * 10
        this.enemyHealth = this.enemyHealth - this.damageNumber
      }
    },
    selectSkill2() {
      if (this.diceSelected == true) {
        const usedDice = this.dice[this.indexNumber]
        this.dice = this.dice.filter((d) => d !== usedDice)
        this.healNumber = this.diceNumber * 5
        this.playerHealth = this.playerHealth + this.healNumber
      }
    },
    reloadDice() {
      if (this.dice.length === 0) {
        for (let i = 0; i < 4; i++) {
          let randomNumber = Math.floor(Math.random()*6)+1
          this.dice.push({number: randomNumber})
        }        
      }
    }
  },
  mounted() {
    for (let i = 0; i < 4; i++) {
    let randomNumber = Math.floor(Math.random()*6)+1
    this.dice.push({number: randomNumber})
    }
  },
  updated() {
    if (this.dice.length == 0) {
      for (let i = 0; i < 4; i++) {
        let randomNumber = Math.floor(Math.random()*6)+1
        this.dice.push({number: randomNumber})
      }
    }
  }
}
</script>

<style scoped>
.game-field {
  display: flex;
}

.game-dice {
  display: flex;
}

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

.hide {
  display: none;
}

p {
  margin: 0;
}

</style>