<template>
    <main class="container my-5">
        <div class="row">
            <div class="col-12 text-center my-3">
                <h3 class="mb-3 display-4 text-uppercase">Reservar Computador</h3>
        </div>

        <div class="col-12 text-center my-3 ">
            <form @submit.prevent="adicionaReserva">
                <div class="form-group">
                    <label >Data</label>
                    <input type="date" class="form-control" v-model="reserva.data">
                </div>
                
                <div class="form-group">
                    <label for>Horario</label>
                    <select class="form-control" v-model="reserva.horario">
                        <option value="1">08:00 às 09:00</option>
                        <option value="2">09:00 às 10:00</option>
                        <option value="3">10:00 às 11:00</option>
                        <option value="4">13:00 às 14:00</option>
                        <option value="5">14:00 às 15:00</option>
                        <option value="6">15:00 às 16:00</option>
                        <option value="7">16:00 às 17:00</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for>Computador</label>
                    <select class="form-control" v-model="reserva.id_computador">
                        <option v-for="computador in computadores" v-bind:value="computador.id">{{computador.descricao}}</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for>Aluno</label>
                    <select class="form-control" v-model="reserva.id_aluno" >
                        <option v-for="aluno in alunos"  v-bind:value="aluno.id">{{aluno.name}}</option>
                    </select>
                </div>
                <button type="submit" class="btn btn-primary">Adicionar</button>
            </form>
        </div>
        </div>
    </main>
</template>
<script>

export default {
    head(){
        return{
            title: "Reservar computador"
        };
    },
    async asyncData({ $axios, params}){
        try{
            let alunos  = await $axios.$get(`/aluno/`);
            let computadores = await $axios.$get(`/computador/`);
            return {alunos, computadores};
        }catch (e){
            return {alunos:[], computadores:[]};
        }
    },
    data(){
        return{
            alunos:[],
            computadores:[],
            reserva:{
                data:"",
                horario: "",
                id_computador: "",
                id_aluno: ""
            }         
        };
    },
    methods:{
        async adicionaReserva(){
            const config = {
                headers: {"content-type": "multipart/form-data"}
            };
            let formData = new FormData();
            for (let data in this.reserva){
                formData.append(data, this.reserva[data]);
            }
            
            try{
                let response = await this.$axios.$post("/reserva/", formData, config);
                this.$router.push("/");
                return alert("Agendamento concluido!");
            }catch(e){
                console.log(e);
            }
        }
    }
}
</script>
<style scoped>
</style>