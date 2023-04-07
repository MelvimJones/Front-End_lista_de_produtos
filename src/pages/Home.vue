

<template>
    <div class="gradient">
        <v-container>
            <v-row no-gutters>
                <v-col v-for="(prod, i ) in produtos" :key="i">
                    <div id="cad">
                        <v-img :src="prod.imagem" center contain :alt="prod.descricao" width="200" height="200" />
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
            searchTerm: '',
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
<!--
    codigos antigos

    background: linear-gradient(45deg, #6096B4, #93BFCF, #BDCDD6, #EEE9DA);    
    width: 100vh;
    height: 100vh;
  -->
  
<style>
.gradient {
    margin-top: 57px;
    display: flex;
    background: linear-gradient(45deg, #FFFFD2, #E4E4E4, #8293FF, #503BFF);
    background-size: 400% 400%;
    background-repeat: no-repeat;
    animation: colors 20s ease infinite;
    flex-direction: row;
    align-items: flex-start;
}

#cad {
    background-color: #ffffff;
    box-shadow: 0.1px 0.5px 20px #5c5858d1;
    padding: 10px;
    margin: 10px 9px 0 9px;
    height: 300px;
    border-radius: 20px;

    display: flex;
    align-items: center;
    flex-direction: column;

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

#img1 {
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>