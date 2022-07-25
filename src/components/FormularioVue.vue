<template>
    <div>
        <form @submit.prevent="registrar">
            <h2>Registrarse</h2>
            <div class="form-group">
                <div class="row">
                    <div class="col">
                        <label class="form-label text-start">Nombre</label>
                        <input type="text" class="form-control" placeholder="Nombre" v-model.trim.lazy="nombre">
                        <div v-if="errors.find(e => e.id === 'nombre')" class="form-error validationError">{{errors.find(e => e.id === 'nombre').msg}}</div>
                    </div>
                    <div class="col">
                        <label for="inputPais" class="form-label text-start">Apellido</label>
                        <input type="text" class="form-control" placeholder="Apellido" v-model.trim.lazy="apellido">
                        <div v-if="errors.find(e => e.id === 'apellido')" class="form-error validationError">{{errors.find(e => e.id === 'apellido').msg}}</div>
                    </div>
                </div>
            </div>
            <br>
            <div class="form-group">
                <label class="form-label text-start">Fecha de Nacimiento</label>
                <input type="date" v-model="nacimiento" class="form-control">
                <div v-if="errors.find(e => e.id === 'nacimiento')" class="form-error validationError"> {{errors.find(e => e.id === 'nacimiento').msg}}</div>
            </div>
            <br>
            <div class="form-group">
                <label class="form-label text-start">Nro. Rifa Elegido</label>
                <input type="number" class="form-control" placeholder="Nro. Rifa" v-model.trim.lazy="rifa">
                <div v-if="errors.find(e => e.id === 'rifa')" class="form-error validationError"> {{errors.find(e => e.id === 'rifa').msg}}</div>
            </div>
            <br>
            <div class="form-group">
                <label class="form-label text-start">Mail</label>
                <input type="email" class="form-control" placeholder="Email" v-model.trim.lazy="mail">
                <div v-if="errors.find(e => e.id === 'mail')" class="form-error validationError"> {{errors.find(e => e.id === 'mail').msg}}</div>
            </div>
            <br>
            <div class="form-group">
                <button type="submit" class="btn btn-success btn-lg btn-block">Registrarse</button>
            </div>
        </form>
    </div>
</template>

<script>
/* eslint-disable */ 
  export default {
    name: 'RegisterPage',
    props: {
        UsuariosRegistrados: Array
    },
    data() {
        const nombre = ''
        const apellido = ''
        const today = new Date()
        const nacimiento = moment(String(today)).format('YYYY-MM-DD')
        const rifa = 0
        const mail = ''
        const errors = []
        return {
        nombre,
        apellido,
        nacimiento,
        rifa,
        mail,
        errors
        }
    },
    methods: {
        registrar(){
            if(this.registroOk()){
                this.guardarUsuarioNuevo()
                this.clearForm()
                this.$emit("RegistroTerminado")
            }
        },
        registroOk(){
            this.errors = []
            if(this.nombre === "") {
                this.errors.push({id:"nombre", msg: "Nombre requerido"})
            }
            if(this.apellido === "") {
                this.errors.push({id:"apellido", msg: "Apellido requerido"})
            }
            if(moment().diff(this.nacimiento, 'years') < 18) {
                this.errors.push({id:"nacimiento", msg: "Debe ser mayor de edad"})
            }
            if(this.rifa === 0) {
                this.errors.push({id:"rifa", msg: "Nro. de rifa requerido"})
            }
            if(this.mail === "") {
                this.errors.push({id:"mail", msg: "Mail requerido"})
            }
            if(this.errors.length === 0){
                return true
            }else{
                return false
            }
        },
        guardarUsuarioNuevo(){
            const registroNuevo = {
                nombre: this.nombreCompleto,
                nacimiento: moment(String(this.nacimiento)).format('DD/MM/YYYY'),
                rifa: this.rifa,
                mail: this.mail
            }
            this.$props.UsuariosRegistrados.push(registroNuevo)
        },
        clearForm(){
            this.nombre = ''
            this.apellido = ''
            this.nacimiento = new Date()
            this.rifa = 0
            this.mail = ''
        },
    },
    computed: {
        nombreCompleto() {
            return `${this.nombre} ${this.apellido}`
        }
    }
}
</script>
<style scoped>
.validationError {
    color: red;
}
</style>