<template>
    <main class="d-flex align-items-center">
        <GooseGrid/>
        <DiceSection/>
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
