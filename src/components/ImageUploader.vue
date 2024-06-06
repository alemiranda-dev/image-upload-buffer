<template>
    <!-- ATENÇÃO, NÃO ME PREOCUPEI MTO COM O FRONT hehehehe -->
    <div id="app">
        <h1>Buffer</h1>
        <h3>Upload e exibição de imagem utilizando buffer</h3>
        <input type="file" @change="onFileChange" />
        <div v-if="imageSrc" class="classImageUpload">
            <h2>Imagem carregada:</h2>
            <img :src="imageSrc" alt="Uploaded Image" style="border-radius: 10px;"/>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            imageSrc: null,
        };
    },
    methods: {
        onFileChange(event) {
        const file = event.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = (e) => {
                // Converte a imagem para buffer
                const arrayBuffer = e.target.result;
                const buffer = new Uint8Array(arrayBuffer);

                // Cria um Blob a partir do buffer e gera uma URL para exibição
                const blob = new Blob([buffer], { type: file.type });
                this.imageSrc = URL.createObjectURL(blob);
            };
            reader.readAsArrayBuffer(file);
        }
        },
    },
};
</script>

<style scoped>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #FFF;
    }

    .classImageUpload{
        background: #ffffff2f;
    }

    img {
        max-width: 20%;
        height: auto;
    }
</style>