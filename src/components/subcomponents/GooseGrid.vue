<template>
    <section id="goose-grid-section" class="d-flex flex-wrap flex-shrink-0">
        <img :key="'A'+ index" v-for="(player, index) in players" 
            :id="player.id" :src="player.src" :alt="player.alt" :class="(player.stop) ? 'bg-danger' : ''">
        <div class="box d-flex justify-content-center align-items-center" :key="index" v-for="(box,index) in boxes"
            :class="`box-${box.boxType}`">
            <h1 class="m-0">{{box.boxID}}</h1>  
        </div>
        <div v-if="winner!=undefined" class="winner-container rounded d-flex flex-column align-items-center justify-content-end py-5">
                <h3 class="bg-light rounded p-3">{{winner}} ha catturato il CyberCriminale!</h3> 
                <button class="btn btn-lg">Play Again</button>
        </div>
    </section>
</template>
<script>

export default {
    name : 'GooseGrid',
    data: function () {
        return {
            boxes : [],
            players : [
                {
                    id : 'cyberino',
                    src : require('./../../assets/Cyberino-nowriting.png'),
                    alt : 'cyberino logo',
                    colCounter : 0,
                    rowCounter : 0,
                    stop: false
                },
                {
                    id : 'super-bite',
                    src : require('./../../assets/Digitalia-nowriting.png'),
                    alt : 'super bite logo',
                    colCounter : 0,
                    rowCounter : 0,
                    stop: false
                },
                {
                    id : 'securya',
                    src : require('./../../assets/Securya-nowriting.png'),
                    alt : 'securya logo',
                    colCounter : 0,
                    rowCounter : 0,
                    stop: false
                },
                {
                    id : 'digitalia',
                    src : require('./../../assets/SuperByte-nowriting.png'),
                    alt : 'digitalia logo',
                    colCounter : 0,
                    rowCounter : 0,
                    stop: false
                }
            ],
            winner : undefined
        }
    },
    created() {
        this.$root.$refs.GooseGrid = this;
    },
    methods : {
        /**
         * Devo fare le classi per settare colCounter e rowCounter
         * poi devo assegnare un v:bind al top e al left collegato a rowCounter e ColCounter
         */
        moveLeft(index){
            this.players[index].colCounter++
            const playerIcon = document.querySelector(`#${this.players[index].id}`)
            if(this.players[index].colCounter % 9 === 0)
                this.moveDown(playerIcon, index)    
            else
                playerIcon.style.left = 'calc((75vh / 9) * '+this.players[index].colCounter+')'
            
            if(this.players[index].rowCounter > 9){
                this.winner = this.players[index].id
            }
        },
        moveBack(index){
            this.players[index].colCounter--
            const playerIcon = document.querySelector(`#${this.players[index].id}`)
            if(this.players[index].colCounter % 9 === 0)
                this.moveUp(playerIcon, index)    
            else
                playerIcon.style.left = 'calc((75vh / 9) * '+this.players[index].colCounter+')'
        },
        moveDown(playerIcon, index){
            this.players[index].rowCounter++
            this.players[index].colCounter = 0
            playerIcon.style.left = 0
            playerIcon.style.top = 'calc((75vh / 9) * '+this.players[index].rowCounter+')'
            
        },
        moveUp(playerIcon, index){
            this.players[index].rowCounter--
            this.players[index].colCounter = 9
            playerIcon.style.left = 'calc((75vh / 9) * '+this.players[index].colCounter+')'
            playerIcon.style.top = 'calc((75vh / 9) * '+this.players[index].rowCounter+')'
            
        }
    },
    mounted(){
        for (let i = 0; i < 81; i++) {
            let type = ''
            if(i === 6 || i === 14 || i === 18 || i === 24 ||i === 32 || i === 37 ||i === 42 ||i === 45 ||i === 59 || i === 64 || i === 75 || i === 79)
                type = 'stop'
            else if(i === 10 || i === 15 || i === 19 || i === 25 || i === 39 || i === 49 || i === 56 || i === 50 || i === 65)
                type = 'back'
            else
                type = 'default'
            this.boxes.push({
                boxID : i,
                boxType : type
            })
        }
    },
    updated(){

    }
}
</script>
 <style scoped lang="sass">
    $box-1x1 : calc(75vh / 9)
    #goose-grid-section
        width: $box-1x1 * 9 //80px width of single box, 0 sqrt of 81 (for index)
        position: relative
    .box
        height: $box-1x1
        width: $box-1x1
        border: solid 1px #036507
        h1
            font-size: $box-1x1 - 10vh
            font-weight: bold
            color: rgba(255, 255, 255, 0.8)
    .box-default
        background-color: rgba(3, 101, 7, 0.6)
    .box-stop
        background-color: rgba(181, 12, 0, 0.6)
    .box-back
        background-color: rgba(255, 255, 0, 0.6)
    img 
        position: absolute
        top: 0
        left: 0
        width: $box-1x1
        height: $box-1x1
        transition: 1s
        border-radius: 50%
        border: solid #00e264
        object-fit: contain
    .winner-container
        position: absolute
        top: 0
        right: 0
        left: 0
        bottom: 0
        background-image: url('./../../assets/winner-image.jpeg')
        background-size: contain
        background-repeat: no-repeat
        background-position: right top
        background-color: #f04d46
        border: solid white
        button
            background-color: #00abcd
            color: white
            &:hover
                color: #00abcd
                background-color: white
                border-color: #00abcd

 </style>