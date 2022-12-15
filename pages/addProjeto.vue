<template>
    <main class="container my-5">
        <div class="row">
            <div class="col-12 text-center my-3">
                <h2 class="mb-3 display-4 text-uppercase">Adicionar Projeto</h2>
        </div>
        <div class="col-2"></div>
        <div class="col-8 text-center my-3 ">
            <form @submit.prevent="adicionaProjeto">
                <div class="form-group">
                    <label >Titulo</label>
                    <input type="text" class="form-control" v-model="projeto.titulo">
                </div>
                <div class="form-group">
                    <label >Descricao</label>
                    <input type="text" class="form-control" v-model="projeto.descricao">
                </div>
                <div class="form-group">
                    <label >Data Inicio</label>
                    <input type="date" class="form-control" v-model="projeto.dataInicio">
                </div>
                <div class="form-group">
                    <label >Data Fim</label>
                    <input type="date" class="form-control" v-model="projeto.dataFim">
                </div>
                <div class="form-group">
                    <label for>Coordenador</label>
                    <select class="form-control" v-model="projeto.coordenador">
                        <option v-for="coordenador in coordenadores" v-bind:value="coordenador.id">{{coordenador.name}}</option>
                        
                    </select>
                </div>
                <button type="submit" class="btn btn-primary">Adicionar</button>
            </form>
        </div>
        <div class="col-2"></div>
        </div>
    </main>
</template>
<script>

export default {
    head(){
        return{
            title: "Criar novo projeto"
        };
    },
    async asyncData({ $axios, params}){
        try{
            let coordenadores  = await $axios.$get(`/coordenador/`);
            return {coordenadores};
        }catch (e){
            return {coordenadores:[]};
        }
    },
    data(){
        return{
            errors: [],
            coordenadores:[],
            projeto:{
                titulo:"",
                descricao: "",
                dataInicio: "",
                dataFim: "",
                coordenador:"",
            }         
        };
    },
    methods:{
        async adicionaProjeto(){
            const config = {
                headers: {"content-type": "multipart/form-data"}
            };
            let formData = new FormData();
            for (let data in this.projeto){
                formData.append(data, this.projeto[data]);
            }
            
            try{
                let response = await this.$axios.$post("/projeto/", formData, config);
                this.$router.push("/coordenador");
                return alert("Projeto criado!");
            }catch(e){
                alert("campos vazios");
            }
        }
    }
}
</script>
<style scoped>
</style>