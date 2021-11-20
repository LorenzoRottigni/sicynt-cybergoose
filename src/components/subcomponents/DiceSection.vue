<template>
    <section id="dice-section" class="p-5">
        <div class="d-flex gap-5">
            <div id="dice-1" class="dice d-flex flex-wrap justify-content-around align-items-around">
                <i :key="index" v-for="(item, index) in diceRollNumber1" class="fas fa-dot-circle w-50 d-flex justify-content-center align-items-center"></i>
            </div>
            <div id="dice-2" class="dice d-flex flex-wrap justify-content-around align-items-around">
                <i :key="index" v-for="(item, index) in diceRollNumber2" class="fas fa-dot-circle w-50 d-flex justify-content-center align-items-center"></i>
            </div>
        </div>

        <div class="d-grid">
            <button @click="roll()" class="btn btn-lg btn-outline-danger btn-block mt-5"> SPIN </button>
        </div>
        <h3 class="text-center mt-3">{{this.$root.$refs.GooseGrid.players[currentUser].id}} turn</h3>
        <SecurityAdvisor v-if="advisorHandler" @adviceSatus="toggleAdvisor"></SecurityAdvisor>
    </section>
</template>
<script>
    import SecurityAdvisor from './SecurityAdvisor.vue'

    export default{
        name : 'DiceSection',
        data(){
            return {
                diceRollNumber1 : undefined,
                diceRollNumber2 : undefined,
                currentUser : 0,
                advisorHandler : false 
            }
        },
        components : {
            SecurityAdvisor
        },
        methods : {
            roll(){
                const isStopped = this.$root.$refs.GooseGrid.players[this.currentUser].stop
                if(!isStopped){
                    let loopCounter = 0
                    const diceLoop = setInterval(()=>{
                        loopCounter++
                        this.diceRollNumber1 = Math.floor(Math.random()*6) + 1
                        this.diceRollNumber2 = Math.floor(Math.random()*6) + 1
                        this.rollAnimation('#dice-1')
                        this.rollAnimation('#dice-2')
                        if(loopCounter === 6){
                            clearInterval(diceLoop)
                            setTimeout(()=>{
                                this.move(this.currentUser,this.diceRollNumber1+this.diceRollNumber2)
                                this.checkPlayerBox()
                                this.changeUser()
                            }, 2000)
                            
                        }   
                    }, 1000)
                }else{
                    this.$root.$refs.GooseGrid.players[this.currentUser].stop = false
                    this.changeUser()
                }
                
            },
            changeUser(){
                if(this.currentUser === 3)
                        this.currentUser = 0
                    else
                        this.currentUser++
                
                
            },
            move: function(index, diceNumber) {
                for (let i = 0; i < diceNumber; i++) {
                    this.$root.$refs.GooseGrid.movePlayer(index)
                    
                }
                
            },
            moveBack: function(index, diceNumber) {
                for (let i = 0; i < diceNumber; i++) {
                    setTimeout(()=> this.$root.$refs.GooseGrid.movePlayerBack(index), 3000)
                   
                }
                
            },
            checkPlayerBox(){
                let userPositionX = this.$root.$refs.GooseGrid.players[this.currentUser].colCounter
                let userPositionY = this.$root.$refs.GooseGrid.players[this.currentUser].rowCounter
                let userPosition = (userPositionY*9) + userPositionX 
                let boxType = this.$root.$refs.GooseGrid.boxes[userPosition].boxType
                if(boxType === 'back'){
                    this.moveBack(this.currentUser,2)
                    this.advisorHandler = true
                }else if(boxType === 'stop'){
                    this.$root.$refs.GooseGrid.players[this.currentUser].stop = true
                    this.advisorHandler = true
                }
            },
            rollAnimation(diceSelector){
                const dice = document.querySelector(diceSelector)
                dice.animate([
                    // keyframes
                    { transform: 'rotateZ(0)' },
                    { transform: 'rotateZ(360deg)' }
                ], {
                    // timing options
                    duration: 1000,
                    iterations: 1
                });
            },
            toggleAdvisor(){
                this.advisorHandler = false
            }

        }
    }
</script>
<style scoped lang="sass">   
h3
    color: #b50c00
@keyframes spin 
    0%
        transform: rotateZ(0)
    100%
        transform: rotateZ(360deg)
#dice-section
    background-color: rgba(255,255,255, 0.7)
    border-radius: 25px
    border: solid 1px #b50c00
    position: relative
.dice
    width: 20vh
    height: 20vh
    border: ridge 15px #b50c00
    border-radius: 1.5rem
    transition: 6s
    background-color: white
    i
        color: #b50c00
.bg-danger
    background-color: #b50c00 !important
.btn-outline-danger 
    color: #b50c00 !important
    border-color: #b50c00 !important
.btn-outline-danger:hover 
    color: #fff !important
    background-color: #b50c00 !important
    border-color: #fff !important


</style>