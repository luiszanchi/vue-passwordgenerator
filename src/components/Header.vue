<template>
    <div>
        <b-navbar toggleable="lg" variant="primary" class="navbar">
            <b-navbar-brand class="about" href="#" @click="openModal = true">
                Sobre
            </b-navbar-brand>
            <b-navbar-brand class="title" href="">
                Gerador de Senhas
            </b-navbar-brand>
        </b-navbar>
        
        <b-modal :visible="openModal" cancel-disabled content-class="shadow" title="Sobre" @hide="openModal = false">
            <p class="my-2">
                Desenvolvido por Luis Zanchi
            </p>
            <p class="my-2">
                <a target="_blank" :href="links.linkedin"> 
                    <b-icon-linkedin
                        style="color: #000000;"
                    /> 
                </a>
                {{ links.linkedin }}
            </p>
            <p class="my-2">
                <a :href="'mailto:' + links.email">
                    <b-icon-google
                        style="color: #000000;"
                    />
                </a>
                {{ links.email }}
            </p>
            <template #modal-footer="{ hide }">
                <b-button size="md" @click="hide()">
                    OK
                </b-button>
            </template>
        </b-modal>
    </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
    name: "Header",
    data: () => ({
        openModal: false,
        links: {
            linkedin: 'https://www.linkedin.com/in/luis-zanchi-7400b5a5/',
            email: 'lftzanchi@gmail.com',
        }
    })
})
</script>

<style lang="scss" scoped>
.navbar {
    display: block;
}
.about {
    float: right;
}
.title {
    display: flex;
}
</style>