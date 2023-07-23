<template>
    <div id="OpinionesView">
        <h1>Componente opiniones</h1>
        <p>Escribe tu opinion para el juego: {{ nombre }}</p>
        <hr>
        <div class="container" id="divform">
            <form>
            <div class="mb-3">
                <label for="txtnombre" class="form-label">Nombre:</label>
                <input type="text" class="form-control" id="txtnombre" v-model="nombreEnviado" aria-describedby="txtnombreHelp">
                <div id="txtnombreHelp" class="form-text">Ingrese su nombre para la opinión.</div>
            </div>
            <div class="mb-3">
                <label for="txtopinion" class="form-label">Opinión:</label>
                <input type="text" class="form-control" id="txtopinion" v-model="opinionEnviada">
            </div>
           
            <button type="submit" v-on:click.prevent="agregaropinion()" class="btn btn-info">{{ nombreBoton }}</button>
        </form>

        </div>
        
        <hr>
        <div class="container">
            <h2>A continuación podrás ver tu opinión</h2>
                <div id="sinopiniones" v-if="cantidadopiniones<1">
                    <p>No existen opiniones para mostrar</p>
                    
            

                </div>
                <hr>
        
                <div class="accordion" id="accordionExample" v-if="cantidadopiniones>0">
                    <div class="accordion-item" v-for="(elemento,index) in opiniones">
                        <h2 class="accordion-header">
                        <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target= "#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                          Opinión creada por: {{ elemento.nombre }}
                        </button>
                        </h2>
                        <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
                        <div class="accordion-body">
                            {{ elemento.opinion }}
                        </div>
                        <button class="btn btn-danger" v-on:click="eliminarOpinion(index)">Eliminar</button>
                        <button class="btn btn-warning " v-on:click="editarOpinion(index)">Editar</button>
                        </div>
                        
                    </div>
                    
                    
                </div>
        </div>

        
        

        
        <router-link to="/">Volver</router-link> 

    </div>
</template>

<script>
export default{
    name: 'OpinionesView',
    props:['nombre'],
    data: function(){
        return{
            cantidadopiniones: 0,
            nombreEnviado: '',
            opinionEnviada: '',
            opiniones:[],
            nombreBoton: 'Agregar',
            indiceActualizar: 0,
         
            

        }
    },
    methods:{
        agregaropinion:function(){
            if(this.nombreBoton == 'Agregar'){
                this.cantidadopiniones++;
            let nuevaopinion={
                nombre:this.nombreEnviado,
                opinion:this.opinionEnviada,
            };
            this.opiniones.push(nuevaopinion);
            this.nombreEnviado='';
            this.opinionEnviada='';

            }
            else if(this.nombreBoton == 'Actualizar'){
                let opinionActualizada={
                    nombre:this.nombreEnviado,
                    opinion:this.opinionEnviada,

                };
                this.opiniones.splice(this.indiceActualizar,1, opinionActualizada);

            }



           

        },
        eliminarOpinion:function(indice){
            this.cantidadopiniones--;
            this.opiniones.splice(indice,1);

        },
        editarOpinion:function(indice){
            this.nombreEnviado=this.opiniones[indice].nombre;
            this.opinionEnviada=this.opiniones[indice].opinion;
            this.nombreBoton = 'Actualizar';
            this.indiceActualizar = indice;
        },

    }
}

</script>

<style scoped>

#OpinionesView{
    background-color: yellowgreen;
}
#divform{
    background-color: lightblue;
    text-align: start;
}
#sinopiniones{
    border: 2px solid rosybrown;
    background-color: lightpink;
    color: brown;
    border-radius: 10px;
}

</style>