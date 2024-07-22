<template>
    <div id="app">
        <main class="my-5 container">
            <div class="row">
                <div class="col-3">
                    <!-- Acá ingresamos los props, que es pasarle la información que yo quiero desde el componente padre al hijo -->
                    <CardPerson :usuario="usuarios[0]" @enviarMensaje="enviarMensajeHandler" />
                </div>
                <div class="col-6 d-flex">
                    <ChatUsers :mensajes="mensajes" :usuarios="usuarios" />
                </div>
                <div class="col-3">
                    <!-- Acá ingresamos los props, que es pasarle la información que yo quiero desde el componente padre al hijo -->
                    <CardPerson :usuario="usuarios[1]" @enviarMensaje="enviarMensajeHandler" />
                </div>
            </div>
        </main>
    </div>
</template>

<script>

// Imports
import axios from "axios";
import CardPerson from "./components/CardPerson.vue";
import ChatUsers from "./components/ChatUsers.vue";

// Exports
export default {
    name: "App",
    components: {
        CardPerson,
        ChatUsers,
    },

    //
    data() {
        return {
            usuarios: [],
            mensajes: [],
        };
    },

    // Este método es el que llama a la información de la Api, por eso usamos Axios.get
    methods: {
        async getPerson() {
            try {
                let response = await axios.get("https://randomuser.me/api/?results=2");
                this.usuarios = response.data.results;
            } catch (error) {
                console.log(error);
            }
        },
        enviarMensajeHandler(mensaje) {
            let nuevoMensaje = {
                id: mensaje.id,
                color: mensaje.color,
                nombreCompleto: mensaje.nombreCompleto,
                texto: mensaje.texto,
            };
            this.mensajes.push(nuevoMensaje);
        },
    },

    // Este método de ciclo de vida, le estoy diciendo a la app vue que apenas me monte el DOM ejecute la función getPerson
    mounted() {
        this.getPerson();
    },
};
</script>

<style scoped>
* {
    font-family: "Lato", sans-serif;
    font-weight: 400;    
}
</style>