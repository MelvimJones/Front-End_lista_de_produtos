
<!-- <template>
    <div class="gradient">
        <v-row no-gutters align="center" justify="center">

            <v-col v-for="(prod, i ) in produtos" :key="i" cols="3">
                <v-sheet class="pa-2 ma-2" align="center" justify="center">
                    <v-img :src="prod.imagem" :alt="prod.descricao" width="200" height="200" />
                    <v-sheet class="ma-2 pa-2">
                        {{ prod.descricao }}
                    </v-sheet>
                </v-sheet>
            </v-col>

        </v-row>
    </div>
</template> -->

<template>
    <div class="gradient">
        <v-container>
            <v-row no-gutters>

                <v-col v-for="(prod, i ) in produtos" :key="i" cols="3">
                    <div id="cad">
                        <v-img :src="prod.imagem" :alt="prod.descricao" width="200" height="200" />
                        <v-sheet id="descricao" class="ma-2 pa-2">
                            {{ prod.descricao }}
                        </v-sheet>
                    </div>
                </v-col>
            </v-row>
        </v-container>
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
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background: linear-gradient(45deg, #6096B4, #93BFCF, #BDCDD6, #EEE9DA);
    background-size: 300% 300%;
    animation: colors 5s ease infinite;
}

#cad {
    background-color: #ffffff;
    padding: 10px;
    margin: 5px 9px;
    height: 300px;
    border-radius: 20px;
}

#descricao {
    text-align: center;
}


@keyframes colors {
    0% {
        background-position: 0% 50%;
    }

    50% {
        background-position: 100% 50%;
    }

    100% {
        background-position: 0% 50%;
    }

}

.my-component {}

#card {
    display: flex;
    flex-wrap: wrap;
    align-content: stretch;
    flex-direction: row;
}

#produtos {
    margin: 12px 0;
    font-size: 1rem;


}

#desc {
    display: flex;
    flex-wrap: wrap;
    align-content: stretch;
    flex-direction: row;
}
</style>