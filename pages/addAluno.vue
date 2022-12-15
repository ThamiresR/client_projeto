<template>
    <main class="container my-5">
        <div class="row">
            <div class="col-12 text-center my-3">
                <h3 class="mb-3 display-4 text-uppercase">Adicionar novo aluno</h3>
        </div>

        <div class="col-12 text-center my-3 ">
            <form @submit.prevent="adicionaAluno">
                <div class="form-group">
                    <label >Nome</label>
                    <input type="text" class="form-control" v-model="aluno.name">
                </div>
                <div class="form-group">
                    <label >Email</label>
                    <input type="mail" class="form-control" v-model="aluno.email">
                </div>
                <div class="form-group">
                    <label >Login</label>
                    <input type="text" class="form-control" v-model="aluno.login">
                </div>
                <div class="form-group">
                    <label>Senha</label>
                    <input type="password" class="form-control" v-model="aluno.senha">
                </div>
                <button type="submit" class="btn btn-primary">Entrar</button>
            </form>
        </div>
        </div>
    </main>
</template>
<script>
export default {
    head(){
        return{
            title: "Adicionar novo aluno"
        };
    },
    data(){
        return{
            aluno:{
                name:"",
                email: "",
                login: "",
                senha: "",
            }         
        };
    },
    methods:{
        async adicionaAluno(){
            const config = {
                headers: {"content-type": "multipart/form-data"}
            };
            let formData = new FormData();
            for (let data in this.aluno){
                formData.append(data, this.aluno[data]);
            }
            
            try{
                let response = await this.$axios.$post("/aluno/", formData, config);
                this.$router.push("/coordenador");
                return alert("Novo aluno cadastrado!");
            }catch(e){
                alert("campos vazios");
            }
        }
    }
}
</script>
<style scoped>
</style>