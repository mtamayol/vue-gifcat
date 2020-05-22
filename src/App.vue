<template>
    <div id="app">
        <h1 class="alineaCentro">{{tituloPrincipal}}</h1>

        <form><!-- @submit.prevent="mostrarGatito">-->
            <table class="alineaTabla">
                <tr>
                    <td>
                        <label>Titulo: </label>
                    </td>
                    <td>
                        <input id="titulo" v-model="titulo" type="text"/><!--v-model="texto"-->
                    </td>
                </tr>
                <tr>
                    <td>
                        <label>Filtro: </label>
                    </td>
                    <td>
                        <select name="select" v-model="filtro">
                            <option  v-for="valores in valoresFiltros" :key="valores" >{{valores}}</option>
                        </select>
                    </td>
                </tr>
                <tr>
                    <td>
                        <label>Color: </label>
                    </td>
                    <td>
                        <select name="select" v-model="color">
                            <option v-for="colores in valoresColores" :key="colores">{{colores}}</option>
                        </select>
                    </td>
                </tr>
                <tr>
                    <td>
                        <label>Tama&ntilde;o: </label>
                    </td>
                    <td>
                        <input id="tamanio" v-model="tamanio" type="number"/>
                    </td>
                </tr>
            </table>
            <button class="alineaCentro" @click.prevent="mostrarGatito">Obtener mi gatito</button>
        </form>
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
            color: null,
            tamanio: null,
            valoresFiltros: ['blur', 'mono', 'sepia', 'negative', 'paint', 'pixel'],
            valoresColores: ['rojo', 'azul', 'verde', 'blanco', 'amarillo'],
            colorApi: null

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
                this.traduceColores();
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
            console.log(this.titulo);
            fetch('https://cataas.com/cat/gif/says/' + this.titulo +'?filter=' + this.filtro +'&color=' + this.colorApi +'&size=' + this.tamanio)
                .then(function (response) {
                    console.log("entro al retorno");
                return response.json();
              })
              .then(function(myJson) {
                console.log(myJson);
              });

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

</style>
