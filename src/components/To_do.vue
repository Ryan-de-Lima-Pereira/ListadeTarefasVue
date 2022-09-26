<script>
    export default{
        data(){
            return{
                tarefaInput: '',
                tarefasTo_do: [{
                    titulo: 'Tarefa teste',
                    id: 0,
                    done: false
                }],
                tarefasDone: []
            }
        },
        methods:{
            addTo_do(){
                //console.log('tá funcionando')
                // Adicionando ao To_do
                let tarefa = {
                    titulo: this.tarefaInput,
                    id: this.tarefasTo_do.length + 1,
                    done: false
                }
                this.tarefasTo_do.push(tarefa)
                //Limpando o input
                this.tarefaInput = ''
            },
            changeList(titulo,index,done){
                // Verificar se está no estado fazendo ou não
                if (done == false){
                    // Adicionar no Done
                        let tarefaDone = {
                            titulo: titulo,
                            id: this.tarefasDone.length + 1,
                            done: true
                        }
                        this.tarefasDone.push(tarefaDone)

                    // Retirar da lista To do
                        this.tarefasTo_do.splice(index, 1)

                }else{
                    // Adicionar no To do
                    let tarefaInput = {
                            titulo: titulo,
                            id: this.tarefasTo_do.length + 1,
                            done: false
                        }
                    this.tarefasTo_do.push(tarefaInput)

                    // Retirar da lista To do
                    this.tarefasDone.splice(index, 1)
                }
                
            }
        }
    }

</script>
    
<template>
<main class="container">
    <div class="card">
        <div class="card-content">
            <h2 class="card-header-title title">Lista de tarefas</h2>
        </div>
        <div class="card-content">
            <div class="tile is-ancestor">
                <div class="tile is-parent">
                    <div class="tile is-child box">
                        <p class="title block">Fazer</p>
                        <div class="block">
                            <div class="field has-addons">
                                <div class="control">
                                    <input type="text" class="input block" placeholder="Digite a tarefa aqui" v-model="tarefaInput" @keyup.enter="addTo_do">
                                </div>
                                <div class="control">
                                    <button class="button" @click="addTo_do">
                                        Adicionar
                                    </button>
                                </div>
                            </div>
                            <ul>
                                <li v-for="tarefa, index in tarefasTo_do" :key="index">
                                    <label class="checkbox is-size-5">
                                        <input type="checkbox" @change="changeList(tarefa.titulo,index, tarefa.done)">
                                        {{ tarefa.titulo }}
                                        {{ tarefa.id }}
                                    </label>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
                <div class="tile is-parent">
                    <div class="tile is-child box">
                        <p class="title">Concluido</p>
                        <div class="block">
                            <div class="is-size-5" v-for="tarefa, index in tarefasDone" :key="index">
                                <label class="checkbox">
                                    <input type="checkbox" checked
                                    @change="changeList(tarefa.titulo,index, tarefa.done)"> 
                                    <s> {{ tarefa.titulo }} </s>
                                    {{ tarefa.id }}
                                </label>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</main>
    
</template>

<style>

</style>