<template>
    <section id="goose-grid-section" class="d-flex flex-wrap justify-content-center flex-shrink-0">
        <img :key="'A'+ index" v-for="(player, index) in players" 
            :id="player.id" :src="player.src" :alt="player.alt" :class="(!player.colCounter && !player.rowCounter) ? 'opacity-0' : 'opacity-1'">
        <div class="box d-flex justify-content-center align-items-center" :key="index" v-for="(box,index) in boxes"
            :class="`box-${box.boxType}`">
            <h1 class="m-0">{{box.boxID}}</h1>  
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
                    src : require('./../../assets/Cyberino.png'),
                    alt : 'cyberino logo',
                    colCounter : 0,
                    rowCounter : 0
                },
                {
                    id : 'super-bite',
                    src : require('./../../assets/super-bite.jpeg'),
                    alt : 'super bite logo',
                    colCounter : 0,
                    rowCounter : 0
                },
                {
                    id : 'securya',
                    src : require('./../../assets/securya.png'),
                    alt : 'securya logo',
                    colCounter : 0,
                    rowCounter : 0
                },
                {
                    id : 'digitalia',
                    src : require('./../../assets/digitalia.png'),
                    alt : 'digitalia logo',
                    colCounter : 0,
                    rowCounter : 0
                }
            ]
        }
    },
    created() {
        this.$root.$refs.GooseGrid = this;
    },
    methods : {
        moveLeft(index){
            this.players[index].colCounter++
            const playerIcon = document.querySelector(`#${this.players[index].id}`)
            if(this.players[index].colCounter % 9 === 0)
                this.moveDown(playerIcon, index)    
            else
                playerIcon.style.left = 'calc((60vw / 9) * '+this.players[index].colCounter+')'
        },
        moveDown(playerIcon, index){
            this.players[index].rowCounter++
            this.players[index].colCounter = 0
            playerIcon.style.left = 0
            playerIcon.style.top = 'calc((60vw / 9) * '+this.players[index].rowCounter+')'
            
        }
    },
    mounted(){
        for (let i = 0; i < 81; i++) {
            this.boxes.push({
                boxID : i,
                boxType : 'default'
            })
        }
    }
}
</script>
 <style scoped lang="sass">
    $box-1x1 : calc(60vw / 9)
    #goose-grid-section
        width: $box-1x1 * 9 //80px width of single box, 0 sqrt of 81 (for index)
        margin: 5vw
        position: relative
    .box
        height: $box-1x1
        width: $box-1x1
        border: solid 1px rgb(35, 125, 251)
        h1
            font-size: $box-1x1 - 10vw
            font-weight: bold
            color: rgba(35, 125, 251, 0.5)
    .box-default
        background-color: #eeefec
    img 
        position: absolute
        top: 0
        width: $box-1x1
        height: $box-1x1
        transition: 1s
        background-color: rgba(255,255,255,0.6)
        border-radius: 50%
        border: solid 1px rgb(35, 125, 251)

        

 </style>