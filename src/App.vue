<template>
    <div id="app">
        <section class="section__lavander">
            <h1 class="alineaCentro">{{tituloPrincipal}}</h1>
        </section>
        <section class="section__salmon form__grid">
            <form class="form__padding">
                <!-- @submit.prevent="mostrarGatito">-->
                <table class="alineaTabla">
                    <tr>
                        <td>
                            <label>Titulo: </label>
                        </td>
                        <td>
                            <input id="titulo" v-model="titulo" type="text" /><!--v-model="texto"-->
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <label>Filtro: </label>
                        </td>
                        <td>
                            <select name="select" v-model="filtro" class="largo100">
                                <option v-for="valores in valoresFiltros" :key="valores">{{valores}}</option>
                            </select>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <label>Color: </label>
                        </td>
                        <td>
                            <select name="select" v-model="color" id="hola" @change="traduceColores" class="largo100">
                                <option v-for="colores in valoresColores" :key="colores">{{colores}}</option>
                            </select>

                        </td>
                        <td> <p class="circulo" :style="{'background-color': colorApi}"></p></td>
                    </tr>
                    <tr>
                        <td>
                            <label>Tama&ntilde;o: </label>
                        </td>
                        <td>
                            <input id="tamanio" v-model="tamanio" type="number" />
                        </td>
                    </tr>
                </table>

            </form>
        </section>
        <section class="section__lavander section__padding section__grid">
            <button class="largo100" @click.prevent="mostrarGatito">Obtener mi gatito</button>

            <img id="imgGato" src="" class="img__margin"/>

        </section>
        </div>
</template>

<script>

export default {
    name: 'App',
    data() {
        return {
            tituloPrincipal: 'Random Gif Cat',
            titulo: null,
            filtro: null,
            color: "",
            tamanio: null,
            valoresFiltros: ['blur', 'mono', 'sepia', 'negative', 'paint', 'pixel'],
            valoresColores: ['rojo', 'azul', 'verde', 'blanco', 'amarillo'],
            colorApi: null,
            imagenGatito: null
        }
    },
    methods: {
        mostrarGatito() {
            let esEntero = /^[0-9]+$/;

            if (!this.titulo||!this.color||!this.tamanio) {
                alert("faltan datos");
            }
            else if (!((this.tamanio > 0) && (esEntero.exec(this.tamanio)))) {
                alert("tamanio debe ser entero y positivo");
            } else {          
                this.obtieneGatoAPI();
            }
        },
        traduceColores() {
            if (this.color == 'rojo') {
                this.colorApi = 'red';
            } else if (this.color == 'azul') {
                this.colorApi = 'blue';
            } else if (this.color == 'verde') {
                this.colorApi = 'green';
            } else if (this.color == 'blanco') {
                this.colorApi = 'white';
            } else if (this.color == 'amarillo') {
                this.colorApi = 'yellow';
            }
        },
        obtieneGatoAPI() {
            const url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.colorApi}&size=${this.tamanio}`;
            document.getElementById("imgGato").src = url;
        }
    }
}
</script>

<style>

   #app{
      display: grid;
      justify-content: center;
    }
   button{
       margin-top: 20px;
   }
   .circulo {
     width: 15px;
     height: 15px;
     -moz-border-radius: 50%;
     -webkit-border-radius: 50%;
     border-radius: 50%;
     border: 1px solid grey;
    }
    .largo100 {
        width: 100%;
    }
    .section__lavander {
        background: lavender;
    }
    .section__salmon{
        background: salmon;
    }
    .form__padding{
        padding:20px;
    }
    .alineaCentro{
        text-align:center;
    }
    .section__padding{
        padding: 0px 25px 25px 25px;
    }
    .section__grid{
        display: grid;
        grid-template-columns: 1fr;
        justify-items: center;
    }
    .img__margin{
        margin-top: 20px;
    }
    .form__grid{
        display: grid;
        justify-items: center;
    }
</style>
