<template>
    <div>
        <b-card-group  deck>
            <b-card
            title="Trucs et Astuces"
            class="mb-3 imageDeFond"
            >
                <b-card-text>Rubriques pouvant intéresser</b-card-text>
                    <b-button href="#" class="btn-ouvrir">Ouvrir</b-button>
                </b-card>
        </b-card-group>
    </div>
</template>

<script>
export default {
    
}
</script>

<style scoped>
.btn-ouvrir{
    background-color: rgb(58, 58, 58);
}
.imageDeFond{
    background-image: url('../assets/img/fondSite.jpg');
}
</style>