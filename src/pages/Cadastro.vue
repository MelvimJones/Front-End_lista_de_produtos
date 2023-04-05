<template>
    <div class="gradient">
        <!-- <v-card title="Cadastro" class="mx-auto" max-width="500">
            <v-card-item>
                <v-container fluid>
                    <v-row>
                        <v-col>Descrição</v-col>
                        <v-col>
                            <v-text-field v-model="produto.descricao" />
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>Imagem</v-col>
                        <v-col>
                            <v-text-field v-model="produto.imagem" />
                        </v-col>
                    </v-row>
                </v-container>
            </v-card-item>
            <v-card-actions>
                <v-btn variant="tonal" @click="cancelar()"> cancelar </v-btn>
                <v-btn variant="tonal" @click="salvarProduto()"> salvar </v-btn>
            </v-card-actions>
            <v-alert v-if="mensagens.salvoSucesso" type="success">Salvo com sucesso</v-alert>
            <v-alert v-if="mensagens.excluidoSucesso" type="success">Excluído com sucesso</v-alert>
        </v-card>
        <v-card class="mx-auto" max-width="500" title="Lista de Produtos" subtitle="sucos">
            <v-list>

                <v-list-item v-for="(prod, i ) in produtos" :key="i" active-color="primary" variant="plain"
                    :prependAvatar="prod.imagem" :title="prod.descricao">

                    <v-btn variant="tonal" icon="mdi-delete" @click="deletarProduto(prod._id, i)"></v-btn>
                    <v-btn variant="tonal" icon="mdi-pencil" @click="editarProduto(prod._id, i)"></v-btn>

                </v-list-item>

            </v-list>
        </v-card> -->



        <v-card>
            <v-layout>
                <v-navigation-drawer class="bg-deep-purple" theme="dark" permanent>
                    <v-list color="transparent">
                        <div class="cardCadastro">
                            
                                <v-row>
                                    <v-col>Descrição:</v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="produto.descricao" />
                                    </v-col>
                                </v-row>

                                <v-row>
                                    <v-col>Endereço da Imagem:</v-col>
                                </v-row>
                                <v-row>
                                    <v-col>
                                        <v-text-field v-model="produto.imagem" />
                                    </v-col>
                                </v-row>
                            
                        </div>
                        <v-card-actions>
                            <v-btn variant="tonal" @click="cancelar()"> cancelar </v-btn>
                            <v-btn variant="tonal" @click="salvarProduto()"> salvar </v-btn>
                        </v-card-actions>
                        <v-alert v-if="mensagens.salvoSucesso" type="success">Salvo com sucesso</v-alert>
                        <v-alert v-if="mensagens.excluidoSucesso" type="success">Excluído com sucesso</v-alert>
                    </v-list>

                    <template v-slot:append>
                        <div class="pa-2">
                            <v-btn block>
                                Logout
                            </v-btn>
                        </div>
                    </template>
                </v-navigation-drawer>
                <v-main style="height: 100vh">
                    <!-- MAIN -->

                </v-main>
            </v-layout>
        </v-card>


        <!-- DADOS -->
        <v-card class="mx-auto" max-width="8050">


            <v-list>

                <v-list-item v-for="(prod, i ) in produtos" :key="i" active-color="primary" variant="plain"
                    :prependAvatar="prod.imagem" :title="prod.descricao">

                    <v-btn variant="tonal" icon="mdi-delete" @click="deletarProduto(prod._id, i)"></v-btn>
                    <v-btn variant="tonal" icon="mdi-pencil" @click="editarProduto(prod._id, i)"></v-btn>

                </v-list-item>

            </v-list>
        </v-card>


    </div>
</template>
<script>

import axios from 'axios'

export default {

    name: "ListaProdutos",

    data() {
        return {
            mensagens: {
                salvoSucesso: false,
                excluidoSucesso: false

            },
            produto: {},
            produtos: [],


        };
    },

    methods: {

        async cancelar() {
            this.produto = {}
        },

        async carregarProdutos() {
            //request para API, que retorna uma promisse 
            let request = await axios.get("https://crud-nodejs-teste-a0ntnpfpx-melvimjones.vercel.app/produtos")

            //Ao finalizar o request, carregue os dados em json
            this.produtos = await request.data

            //exibir no consoel
            console.log(this.produtos)
        },

        async salvarProduto() {

            if (this.produto._id == undefined || this.produto._id == "") {
                this.cadastrarProduto()
            } else {
                this.alterarProduto()
            }
            this.cancelar()
            this.mensagens.salvoSucesso = true

            //temporizador
            setTimeout(() => {
                this.mensagens.salvoSucesso = false
            }, 3000);
        },

        async alterarProduto() {
            await axios.put("https://crud-nodejs-teste-a0ntnpfpx-melvimjones.vercel.app/produtos?id=" + this.produto._id, this.produto)
            this.carregarProdutos()
            //alterar na tela
        },

        async cadastrarProduto() {
            let request = await axios.post("https://crud-nodejs-teste-a0ntnpfpx-melvimjones.vercel.app/produtos", this.produto)
            let prod = await request.data
            //altera na tela 
            this.produtos.push(prod)
        },
        async editarProduto(id, i) {

            //acessar do array e colocar no form
            this.produto = { ...this.produtos[i] }
        },

        async deletarProduto(id, i) {
            await axios.delete("https://crud-nodejs-teste-a0ntnpfpx-melvimjones.vercel.app/produtos?id=" + id)

            //excluir do array
            this.produtos.splice(i, 1)

            this.cancelar()
            this.mensagens.excluidoSucesso = true

            //temporizador
            setTimeout(() => {
                this.mensagens.excluidoSucesso = false
            }, 3000);
        }



    },

    async created() {

        console.log("Created....")
        await this.carregarProdutos()
    }

};


</script>
  
<style>
.gradient {
    margin-top: 57px;
    display: flex;
    background: linear-gradient(45deg, #49385d, #FFFFD2, #E4E4E4, #8293FF, #503BFF);
    background-size: 400% 400%;
    background-repeat: no-repeat;
    animation: colors 20s ease infinite;
    flex-direction: row;
    align-items: flex-start;

}

.cardCadastro {
    margin: 10px 10px 1px 10px;
}

.v-col {
    flex-grow: 1;
    max-width: 100%;
}

.bg-deep-purple {
    margin-top: 60px;
}
</style>