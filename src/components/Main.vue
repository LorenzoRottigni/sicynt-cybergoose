<template>
    <main class="d-flex align-items-center justify-content-around flex-grow-1 py-5">
        <GooseGrid/>
        <DiceSection class="align-self-end"/>
    </main>
</template>

<script>
import GooseGrid from './subcomponents/GooseGrid.vue'
import DiceSection from './subcomponents/DiceSection.vue'

export default {
    name : 'Main',
    components : {
        GooseGrid,
        DiceSection
    }
}
</script>

<style scoped lang="sass">


        
</style>
