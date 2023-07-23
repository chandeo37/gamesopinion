<template>


    <div id="Administracion">
        <h1>Componente de administración</h1>
        <div v-if="flagbutton">
            <button class="btn btn-success" v-on:click="mostrarformulario()">Ingresar Datos</button>

        </div>
        <div v-if="flagform" class="container">
            <form>
            <div class="mb-3">
                <label for="txtnombre" class="form-label">Nombre:</label>
                <input type="text" class="form-control" id="txtnombre" v-model="nombreEnviado" aria-describedby="txtnombreHelp">
                <div id="txtnombreHelp" class="form-text">Ingrese su nombre para la opinión.</div>
            </div>
            <div class="mb-3">
                <label for="txtapellido" class="form-label">Apellido:</label>
                <input type="text" class="form-control" id="txtapellido" v-model="apellidoEnviado">
            </div>
           
            <button type="submit" v-on:click.prevent="enviarDatos()" class="btn btn-info">Enviar</button>
        </form>

        </div>
        <div v-if="flagresumen" class="container">
            <div class="row">
                <div id="seccionNombre" class="col-md-3">
                    <p>Bienvenido@</p>
                    <p>{{ nombreEnviado}}  {{ apellidoEnviado }}</p>

                </div>
                <div class="col-md-9">
                    <div class="container">
                        <div class="row">
                            <div class="col-md-12">
                                <h2>Resumen de tu cuenta</h2>
                                <h3>Le diste me gusta al juego:  {{ nombre }}</h3>
                                

                            </div>

                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <p>Sección coins</p>
                                <div id="divcoins" class="container">
                                    <p>¿Deseas comprar coins para este Juego?</p>
                                    <button id="btnCoins" class="btn btn-warning" v-on:click="agregarCoins()"><i class="fab fa-free-code-camp"></i>Agregar coins</button>
                                    <hr>
                                    <p>Cantidad de Coins Comprados</p>
                                    <div class="progress" role="progressbar" aria-label="Example with label" v-bind:aria-valuenow="cantidadCoins" aria-valuemin="0" aria-valuemax="100">
                                        <div class="progress-bar bg-success" style=" ">${{ cantidadCoins }}%</div>
                                    </div>
                                    <div v-if="flagMaximo">
                                        <p class="text-danger">Llegaste al maximo</p>

                                    </div>
                                    <br><br>
                                    
                                </div>
                            </div>
                          

                        </div>
                        <br>
                        <div class="row">
                            <br><br>
                            <hr>
                            <div class="col-md-4 bg-warning">
                                <i class="fas fa-times"></i>
                                <p>% Finalizacion de juego</p>
                                <hr>
                                    <p>17%</p>

                            </div>
                            <div class="col-md-4 bg-success">
                                <i class="fas fa-trophy"></i>
                                <p>Logros en el juego</p>
                                <hr>
                                <p>66%</p>

                            </div>
                            <div class="col-md-4 bg-info">
                                <i class="fas fa-share"></i>
                                <p>Recompensas</p>
                                <hr>
                                <p>200</p>

                            </div>

                        </div>

                    </div>
                    

                </div>
            </div>
            
            <br>
        </div>
        <router-link to="/">Volver</router-link> 
         
    </div>
    
</template>
<script>
export default{
    name: "Administracion",
    props: ["nombre"],
    data: function () {
        return {
            flagform: false,
            flagbutton:true,
            flagresumen:false,
            flagMaximo:false,
            
            nombreEnviado:'',
            apellidoEnviado:'',
            cantidadCoins:0,
            estiloBarra: `width:${this.cantidadCoins}%`,
        }
    },
    methods: {
        mostrarformulario:function(){
            this.flagbutton= false;
            this.flagform=true;

        },
        enviarDatos: function(){
            this.flagform=false;
            this.flagresumen=true;


        },
        agregarCoins: function(){
            this.cantidadCoins++;
            let labarra = document.getElementsByClassName('progress-bar');
            let valorPorCiento='';
            if(this.cantidadCoins <50){
                valorPorCiento = ` ${this.cantidadCoins}%`;
                labarra[0].style.width = valorPorCiento;
                if(this.cantidadCoins>20 && this.cantidadCoins<=30){
                    labarra[0].classList.remove('bg-success');
                    labarra[0].classList.add('bg-warning');
                }
                else if(this.cantidadCoins>30){
                    labarra[0].classList.remove('bg-warning');
                    labarra[0].classList.add('bg-danger');

                }

            }else{
                this.flagMaximo = true;
                let elBotonCoins = document.getElementById('btnCoins');
                elBotonCoins.setAttribute('disabled', true);

            }
            

        },
    },
    
}


</script>

<style scoped>
    #Administracion{
        background-color: rgb(250, 213, 121);
    }
    #seccionNombre{
        background-color: black;
        color: white;
    }
    #divcoins{
        background-color: lightcyan;
        border-radius: 15px;
    }
</style>