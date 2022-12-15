<template>
    <main class="container mt-5">
        <div class="row">
            <div class="col-12 text-right mb-4">
            <div class="d-flex justify-content-between">
                <h3>Área de reservas</h3>
                <nuxt-link to="/addProjeto" class="btn btn-info">Cadastrar Projeto</nuxt-link>
                <nuxt-link to="/addAluno" class="btn btn-info">Adicionar Aluno</nuxt-link>
                <nuxt-link to="/reservar" class="btn btn-info">Reservar horario</nuxt-link>
                </div>
        </div>
        <template >
            <div class="container-xl">
                <div class="table-responsive">
                    <div class="table-wrapper">
                        <div class="table-title">
                            <div class="row">
                                <div class="col-sm-6"><h2>Horarios reservados</h2></div>
                                
                            </div>
                        </div>
                        <table class="table table-striped table-hover table-bordered">
                            <thead>
                                <tr>
                                    <th>#</th>
                                    <th>Data <i class="fa fa-sort"></i></th>
                                    <th>Horas</th>
                                    <th>Computador <i class="fa fa-sort"></i></th>
                                    <th>Aluno</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="horario in horarios" >
                                    <th scope="row">{{ horario.id  }}</th>  
                                    <td>{{ horario.data }}</td> 
                                    <td>{{listaHorario[horario.horario] }}</td> 
                                    <td>{{  computadores[horario.id_computador-1].descricao}}</td>  
                                    <td>{{ alunos[horario.id_aluno-1].name }}</td> 
                                </tr>    
                            </tbody>
                        </table>
                    </div>
                </div>  
            </div>   
        </template>
        </div>
    </main>
</template>


<script>

export default {
    head(){
        return{
            title: "Sistema de reservas"
        };
    },
    async asyncData({ $axios, params}){
        try{
            let alunos  = await $axios.$get(`/aluno/`);
            let computadores = await $axios.$get(`/computador/`);
            let horarios = await $axios.$get(`/reserva/`);
            return {alunos, computadores, horarios};
        }catch (e){
            return {alunos:[], computadores:[]};
        }
    },
    data(){
        return{
            alunos:[],
            computadores:[],
            horarios : [],  
            listaHorario:{
                "1": "08:00 às 09:00",
                "2": "09:00 às 10:00",
                "3": "10:00 às 11:00",
                "4": "13:00 às 14:00",
                "5": "14:00 às 15:00",
                "6": "15:00 às 16:00",
                "7": "16:00 às 17:00",
            },
        };
    },
    methods:{
    }
}
</script>

<style>
</style>