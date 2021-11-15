<template>
    <section id="dice-section">
        <div class="dice d-flex flex-wrap justify-content-around align-items-around">
            <i :key="index" v-for="(item, index) in diceRollNumber" class="fas fa-dot-circle w-50 d-flex justify-content-center align-items-center"></i>
        </div>
        <div class="d-grid gap-2 mt-5">
            <button @click="roll()" class="btn btn-outline-primary btn-block mt-5"> SPIN </button>
        </div>
        

        
    </section>
</template>
<script>
    export default{
        name : 'DiceSection',
        data(){
            return {
                diceRollNumber : undefined,
                currentUser : 0
            }
        },
        methods : {
            roll(){
                this.diceRollNumber = Math.floor(Math.random()*6) + 1
                const dice = document.querySelector('.dice')
                dice.animate([
                    // keyframes
                    { transform: 'rotateZ(0)' },
                    { transform: 'rotateZ(360deg)' }
                ], {
                    // timing options
                    duration: 1000,
                    iterations: 1
                });
                this.move(this.currentUser,this.diceRollNumber)
                if(this.currentUser === 3)
                    this.currentUser = 0
                else
                    this.currentUser++
            },
            move: function(index, diceNumber) {
                for (let i = 0; i < diceNumber; i++) {
                    this.$root.$refs.GooseGrid.moveLeft(index)
                    
                }
                
            }

        }
    }
</script>
<style scoped lang="sass">   
@keyframes spin 
    0%
        transform: rotateZ(0)
    100%
        transform: rotateZ(360deg)
  
.dice
    width: 25vw
    height: 25vw
    border: solid black
    border-radius: 1.5rem
    transition: 6s
</style>