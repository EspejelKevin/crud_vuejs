<template>
    <div class="container">
        <div class="card">
            <div class="card-header">
                Editar empleado
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="editarRegistro">
                    <div class="form-group">
                      <label for="nombre">Nombre:</label>
                      <input type="text"
                        class="form-control" required name="nombre" v-model="empleado.nombre" id="nombre" aria-describedby="helpId" placeholder="Nombre">
                      <small id="helpId" class="form-text text-muted">Escribe el nombre del empleado</small>
                    </div>
                    <br>
                    <div class="form-group">
                      <label for="correo">Correo electrónico:</label>
                      <input type="email"
                        class="form-control" required name="correo" v-model="empleado.correo" id="correo" aria-describedby="helpId" placeholder="Correo">
                      <small id="helpId" class="form-text text-muted">Escribe el correo electrónico del empleado</small>
                    </div>
                    <br>
                    <div class="btn-group" role="group" aria-label="">
                        <button type="sumbit" class="btn btn-success">Modificar</button>
                        <router-link :to="{name:'Listar'}" class="btn btn-warning">Cancelar</router-link>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            empleado:{}

        }
    },
    created:function(){
        this.obtenerDatosEmpleadoByID()
    },
    methods:{
        obtenerDatosEmpleadoByID(){
            fetch("http://localhost/apicrud/?consultar=" + this.$route.params.id)
            .then(respuesta=>respuesta.json())
            .then((datosRepuesta)=>{
                console.log(datosRepuesta)
                this.empleado=datosRepuesta[0];
            })
            .catch(console.log)
        },
        editarRegistro(){
            var datosEnviar = {id:this.empleado.id, nombre:this.empleado.nombre, correo:this.empleado.correo}
            fetch("http://localhost/apicrud/?actualizar="+ this.empleado.id,{
                method:"POST",
                body:JSON.stringify(datosEnviar)
            })
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta=>{
                console.log(datosRespuesta)
                window.location.href="../listar"
            }))
        }
    }
}
</script>