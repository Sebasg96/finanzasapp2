<template>
    <div id="ini_session">    
<!-- Inicio Ventana modal actualizar/Eliminar -->
<script type="text/x-template" id="modal-template">
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
  <!-- Botón Cerrar ventana modal -->
  <button class="modal-default-button" @click="$emit('close')">X</button>
  <!-- cabecera Cerrar ventana modal -->
          <div class="modal-header">
            <slot name="header">
              Mis Datos
            </slot>
          </div>
  <!-- body Cerrar ventana modal -->
          <div class="modal-body">
            <slot name="body">
              <div class="row">
                <div class="col-lg-12">
                  <!-- Formulario Registro-->
                  <form
                    id="register-form"
                    action="#"
                    method="post"
                    role="form"
                    style="display: block"
                  >
                    </div>
                    <div class="form-group">
                      <input
                        type="text"
                        id="nuevo_username"
                        tabindex="1"
                        class="form-control"
                        value={{username}}
                        placeholder="Username"
                      />
                    </div>
                    <div class="form-group">
                      <input
                        type="password"
                        id="nuevo_password"
                        tabindex="2"
                        class="form-control"
                        value={{password}}
                        placeholder="Password"
                      />
                    </div>
                    </div>
                    <div class="form-group">
                      <div class="row">
                        <div class="col-sm-6">
                        <button class="modal-default-button" @click="$emit('eliminar')">Eliminar</button>
                        </div>
                      </div>
                    </div>
                  </form>
                </div>
              </div>
            </slot>
          </div>
<!-- Inicio footer ventana modal -->
          <div class="modal-footer">
            <footer class="page-footer font-small blue pt-4"> 
              <!-- Copyright -->
              <div class="footer-copyright text-center py-3">© 2020 Copyright:<a href="#"> Finir</a>
              </div>
              <!-- Copyright -->
            </footer> 
<!-- Fin footer ventana modal -->                 
          </div>
        </div>
      </div>
    </div>
  </transition>
</script>
<!-- Fin Ventana modal actualizar/Eliminar -->
      <br>
      <br>
      <br>
      <br>
      <br>
<!-- Botón para abrir ventana modal -->      
<button class="btn btn-primary" @click="showModal = true"> 
      <h4 class="text-white text-right ">
        <i class="fas fa-user-cog"></i> Usuario: {{username}} 
      </h4>
</button>
  <!-- usa el componente modal-->
  <modal v-if="showModal" @close="showModal = false" @eliminar="eliminar_usuario">
    <!--
      puedes usar contenido personalizado aquí para sobrescribir
      contenido predeterminado
    -->
    <h3 slot="header">Mis Datos</h3>
  </modal>
      <br>
      <br>
      <br>
<!-- -->
        <div class="container-sm" style="border:0px">
          <div class="row">
              <div class="col-md-6 col-md-offset-3">
                   <div class="panel shadow-lg p-3 mb-5 rounded">
                       <h1 align="center">Bienvenid@ {{nombres}} {{apellidos}}</h1>

                        <div class="panel-heading">
                            <div class="row">
                                <div class="col-xs-12">
                                    <label class="label">Mis finanzas</label>
                                </div>
                            </div>
                            <hr >
                        </div>
                        <!-- Fin cabecera del Panel -->
					<!-- Inicio body del Panel -->
                  <div class="panel-body">
                    <div class="row">
                      <div class="col-lg-12">
                            <div class="container-fluid">
                                <div class="row">
                                  <div class="col-md-6">
                                    <label class="label">Nombre del ítem: </label>
                                  </div>
                                  <div class="col-md-6">
                                    <input name="nombre_item" id="nombre_item" tabindex="2" class="form-control" placeholder="Nombre del item">
                                  </div>
                                </div>
                                <div class="row">
                                  <div class="col-md-6">
                                    <label class="label">Valor: </label>
                                  </div>
                                  <div class="col-md-6">
                                    <input name="valor" id="valor" tabindex="2" class="form-control" placeholder="Valor">
                                  </div>
                                </div>
                                <div class="row">
                                  <div class="col-md-6">
                                    <label class="label">Fecha: </label>
                                  </div>
                                  <div class="col-md-6">
                                    <input name="fecha" id="fecha" tabindex="2" class="form-control" placeholder="fecha">
                                  </div>
                                </div>
                                <div class="row">
                                  <div class="col-md-6">
                                    <label class="label">Tipo: </label>
                                  </div>
                                  <div class=" col-md-6 dropdown">
                                    <button class="btn btn-primary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                                        Seleccione una opción
                                    </button>
                                    <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                                        <a class="dropdown-item" href="#">Action</a>
                                        <a class="dropdown-item" href="#">Another action</a>
                                        <a class="dropdown-item" href="#">Something else here</a>
                                    </div>
                                  </div>
                                </div>
                            </div>
                      </div>
                    </div>
                  </div>        
                  </div>    
              </div>
          </div>
        </div>          
    </div>
</template>

<script>
    import axios from "axios";
    export default{
        name: "ini_session",
        data: function(){
            return{
                nombres: "",
                apellidos: "",
                fecha_registro: "",
                email: "",
                showModal: false,
                nuevo_username:""
            }
        },
        created: function(){
            this.nombres = this.$route.params.nombres
            this.apellidos = this.$route.params.apellidos
            this.username = this.$route.params.username
            this.password = this.$route.params.password
            let self = this
        },
        methods:{
          eliminar_usuario: function(){
            axios.post("https://finanzaspersonales3.herokuapp.com/user/delete/", datos)
                .then((result) => {
                      alert(result.data)
                      this.$router.push({name: "Login"})
                })
                .catch((error) =>{
                  console.log(error)
                })
          }

        }
    }

$(function() {
	$("#finance-form").delay(100).fadeIn(100);

});    
</script>

<style>
.btn{
  margin-left: 10px;
  padding: 5px 5px;
}
/* Estilos de la ventana modal */
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 800px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #59B2E0;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
  color: #fff;
  background-color:#59B2E0;
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
