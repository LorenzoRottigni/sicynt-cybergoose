<template>
    <section class="d-flex align-items-center justify-content-center">
        <div class="advice-container d-flex py-3 px-5 gap-3 flex-column align-items-center justify-content-center rounded">
            <h5 class="text-center">{{advices[activeIndex]}}</h5>
            <button class="btn btn-danger" @click="$emit('adviceSatus')">Ho capito!</button>
        </div>
    </section>
</template>
<script>

export default {
    name : 'SecurityAdvisor',
    data(){
        return {
            advices : [
                'Continua sempre ad aggiornarti sulla sicurezza cyber',
                'Disconnettiti sempre dopo aver terminato le tue transazioni online',
                'Evita il Dark Web',
                'Ferma la diffusione di notizie false! Controllane sempre l\'origine! ',
                'Gestisci al meglio i tuoi PIN personali',
                'Hai un antivirus? La sicurezza inizia sempre dalle domande piu semplici!',
                'Installa Software e App provenienti da sorgenti fidate',
                'Link: non cliccare mai su quelli sconosciuti',
                'Mantieni attivi gli aggiornamenti automatici dei sistemi operativi e delle app che utilizzi',
                'Non cedere con facilita\' le tue informazioni personali',
                'Occhio a quando utilizzi una rete Wi-Fi pubblica ',
                'Per stare sicuro, al termine della navigazione cancella cookies e cronologia',
                'Quando scarichi qualche documento da internet, prima di aprirlo fallo controllare dal tuo antivirus',
                'Rispetta la privacy degli altri utenti',
                'Seguire le regole base di NETiquette puo\' aiutarti a non rovinare le tue relazioni online',
                'Tieni d\' occhio le attività sospette sui tuoi profili utente',
                'Usa l\'autenticazione biometrica o tramite smartphone, se devi usa password commplesse!',
                'Verifica sempre con chi stai interagendo su internet',
                'Zero fiducia: sul web è un sano principio!'
            ],
            activeIndex : undefined
        }
    },
    methods : {
            setActiveIndex(){
                this.activeIndex = Math.floor(Math.random()*19)
            }
    },
    mounted(){
        this.setActiveIndex()
    },
    updated(){
        this.setActiveIndex()
    }
}
</script>
<style scoped lang="sass">
    @keyframes fadeIn 
        0%
            left: 100%,
        100%
            left: 0
    section
        position: absolute
        top: 0
        right: 0
        bottom: 0
        left: 0
        background-color: rgba(181, 12, 0, 0.6)
        border-radius: 25px
        z-index: 99
        animation: fadeIn 2s 1
    .advice-container
        background-color: white
        color: rgba(181, 12, 0, 1)
</style>