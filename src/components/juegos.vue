<template>
    <div id="juegos">

        <h1>Componentes juegos</h1>
        <div class="contenedorpadre">
                <div v-for="(juego,index) in juegos" v:bind:key="index" class="card m-2" style="width: 18rem;">
                    <img v-bind:src="juego.background_image" class="card-img-top" alt="...">
                        <div class="card-body">
                            <h5 class="card-title">{{ juego.name }}</h5>
                            <p class="card-text"> ESRB Rating:  {{ juego.esrb_rating.name }}</p>
                        </div>
                        <ul class="list-group list-group-flush">
                            <li class="list-group-item">Rating:  {{ juego.rating }}</li>
                            <li class="list-group-item">Released: {{ juego.released }}</li>
                            <li class="list-group-item">Updated:  {{ juego.updated }}</li>
                        </ul>
                        <div class="card-body">
                            <a v-on:click="mostrarOpiniones(juego.name)" class="btn btn-primary">Opinar</a>
                            <a v-on:click="irAdministracion(juego.name)" class="btn btn-danger"><i class="fas fa-thumbs-up"></i></a>
                        </div>
                </div>
        </div>

    </div>

</template>

<script>
import axios from 'axios';
export default{
    name:'juegos',
    data:function(){
        return{
            cantidadjuegos:0,
            juegos:[],

        }
    },
    methods:{
        consumirapi:function(){
            let url='https://api.rawg.io/api/games?key=e63f38c751d24ee7b95d829a16ae6142';

            axios(url)
                .then(respuesta =>{
                    console.log(respuesta);
                    console.log(respuesta.data.results[9].name);
                    this.cantidadjuegos=respuesta.data.results.length;

                    for(let i=0; i< respuesta.data.results.length; i++){
                        this.juegos.push(respuesta.data.results[i]);
                    }
                })
                .catch(error=>{
                    console.log(error);
                });

        },
        mostrarOpiniones:function(nombreJuego){
            this.$router.push( `/opiniones/${nombreJuego}` );

        },
        irAdministracion:function(nombreJuego){
            this.$router.push(`/administracion/${nombreJuego}`);

        },

    },
    created(){
        this.consumirapi();

    }
}


</script>

<style scoped>
#juegos{
    background-color: aqua;
}

.contenedorpadre{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}


</style>