<template>
    <div id="card__person" class="container my-5">
        <div class="card">
            <img :src="usuario.picture.large" class="card-img-top" alt="" />
            <div class="card-body">
                <h5 class="card-title">{{ nombreCompleto }}</h5>
                <form>
                    <input class="form-control my-2" type="color" name="color" id="color" v-model="mensaje.color" />
                    <textarea class="form-control my-2" name="chat" id="chat" v-model="mensaje.texto"
                        @keyup.enter="enviarMensaje"></textarea>
                    <br />
                    <!-- Tenemos que hacer un emit a este button porque hay que pasarle información al padre -->
                    <button @click.prevent="enviarMensaje" class="btn btn-primary btn-block w-100">
                        Enviar
                    </button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CardPerson",
    // Props es para recibir desde el padre, ahí queda registrada y queda disponible como si la tuviera dentro de data()
    props: {
        usuario: Object,
    },
    //
    data() {
        return {
            mensaje: {
                texto: "",
                color: "#fff",
                id: "",
            },
        };
    },
    computed: {
        nombreCompleto() {
            return `${this.usuario.name.first} ${this.usuario.name.last}`;
        },
    },
    // Emit es la directiva para mandar datos al padre
    methods: {
        enviarMensaje() {
            this.mensaje.id = this.usuario.id.value;
            this.mensaje.nombreCompleto = this.nombreCompleto;
            this.$emit("enviarMensaje", this.mensaje);
            this.mensaje.texto = "";
        },
    },
    created() {
        console.log(this.usuario);
    },
};
</script>
<style scoped>
* {
    font-family: "Lato", sans-serif;
    font-weight: 400;
}
</style>