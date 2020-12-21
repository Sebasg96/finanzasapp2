<template>
    <div id="ini_session">
        
      <br>
      <br>
      <br>
      <br>
      <br>
      <h4 class="text-white text-right "> Usuario: {{username}}  </h4>

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
                                    <input type="password" name="password" id="password" tabindex="2" class="form-control" placeholder="Contraseña">
                                  </div>
                                </div>
                                <div class="row">
                                  <div class="col-md-6">
                                    <label class="label">Valor: </label>
                                  </div>
                                  <div class="col-md-6">
                                    <input type="password" name="password" id="password" tabindex="2" class="form-control" placeholder="Contraseña">
                                  </div>
                                </div>
                                <div class="row">
                                  <div class="col-md-6">
                                    <label class="label">Fecha: </label>
                                  </div>
                                  <div class="col-md-6">
                                    <input type="password" name="password" id="password" tabindex="2" class="form-control" placeholder="Contraseña">
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
<!-- Logo e icono usuario -->
<script>
    import axios from "axios";
    export default{
        name: "ini_session",
        data: function(){
            return{
                nombres: "",
                apellidos: "",
                fecha_registro: "",
                email: ""
            }
        },
        created: function(){
            this.username = this.$route.params.username
            this.password = this.$route.params.password
            let self = this
            axios.post("https://finanzaspersonales3.herokuapp.com/user/auth/", {
                username: this.username,
                password: this.password
            })
            .then((result) => {
                if (result.data.message){
                    alert(result.data.message)
                }
                else{
                    this.nombres = result.data.nombres
                    this.apellidos = result.data.apellidos
                    this.email = result.data.email
                    this.fecha_registro = result.data.fecha_registro
                }
            })
            .catch((error) =>{
                console.log(error)
                alert("Error del sistema")
            })
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
