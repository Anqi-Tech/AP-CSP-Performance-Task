<template>
    <div class="game">
      <div>
        <div class="game-field">
          <div class="column">
            <h1>You: {{playerHealth}}</h1>
          </div>
          <div class="column">
            <h1 @click="selectSkill1">Deal [number] x 10 damage</h1>
            <h1 @click="selectSkill2">Heal [number] x 5 health</h1>
          </div>
          <div class="column">
            <h1>Your Worst Enemy: {{enemyHealth}}</h1>
          </div>
        </div>
        <div class="game-dice">
          <button v-for="(die, index) in dice" :key="die.id" class="dice" @click="selectDice">
            <p>{{die.number}}</p>
            <p class="hide">{{index}}</p>
          </button>
        </div>
      </div>
      <div>
        <!-- <h1>You win</h1> -->
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
      enemyHealth: 500,
    }
  },
  methods: {
    selectDice(e) {
      if (e.target.tagName == 'BUTTON') {
        this.targetedDice = e.target
      } else {
        this.targetedDice = e.target.parentElement
        console.log(e.target.parentElement.tagName)
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
    if (this.dice.length == 2) {
      this.dice.length = 0
      let takenDamage = Math.floor(Math.random()*30)+10
      this.playerHealth = this.playerHealth - takenDamage
      for (let i = 0; i < 4; i++) {
        let randomNumber = Math.floor(Math.random()*6)+1
        this.dice.push({number: randomNumber})
      }
    }
  }
}
</script>

<style scoped>
.game {
  margin: 5rem;
}

.game-field {
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
}

.column {
  width: 30vw;
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
}

.game-dice {
  display: flex;
  width: 30vw;
  justify-content: center;
}

.dice {
  border: 0.3rem solid black;
  border-radius: 20px;
  width: 5vw;
  aspect-ratio: 1 / 1;
  font-size: 2rem;
  text-align: center;
  margin: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.dice:hover {
  background: rgb(197, 197, 197);
}

.dice:focus {
  border: 0.3rem solid blue;
}

.hide {
  display: none;
}

p {
  margin: 0;
}

</style>