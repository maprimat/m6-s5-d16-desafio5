<template>
    <div id="scrollableDiv" class="container">
        <div v-for="(mensaje, index) in mensajes" :key="index">
            <p :style="{
                textAlign: mensaje.id === usuarios[0].id.value ? 'left' : 'right',
            }">
                <small>{{ mensaje.nombreCompleto }}</small>
            </p>
            <p :style="{
                backgroundColor: mensaje.color,
                textAlign: mensaje.id === usuarios[0].id.value ? 'left' : 'right',
            }">
                {{ mensaje.texto }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: "ChatUsers",
    props: {
        mensajes: Array,
        usuarios: Array,
    },
};
</script>

<style scoped>
#scrollableDiv {
    max-height: 80vh;
    overflow-y: scroll;
    border-radius: 20px;
    box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.2);
}
</style>