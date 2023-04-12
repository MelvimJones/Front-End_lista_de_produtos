# PROJETO CRUD API + Front-end Web Development
#### NodeJS - Express - MongoDB Atlas - JWT - Vue.js - Vuetify

<a href="https://front-end-lista-de-produtos-git-main-melvimjones.vercel.app/" rel="nofollow">Testar / preview</a>

## Front-end em VueJS 3
<div>
<img src="https://github.com/MelvimJones/Front-End_lista_de_produtos/blob/main/src/assets/Tela1.jpg" width="400">

<img src="https://github.com/MelvimJones/Front-End_lista_de_produtos/blob/main/src/assets/Tela2.jpg" width="400">
</div>

## Project setup

```
# yarn
yarn

# npm
npm install

# pnpm
pnpm install
```

### Compiles and hot-reloads for development

```
# yarn
yarn dev

# npm
npm run dev
### Customize configuration

See [Configuration Reference](https://vitejs.dev/config/).
```

FERRAMENTAS USADAS:

<div style="background-color:white">

<img align="center"  height="30" width="40" src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/2560px-Node.js_logo.svg.png" style="max-width: 100%;">
<img align="center" height="30" width="50" src="https://www.edureka.co/blog/wp-content/uploads/2019/05/logo.png" style="max-width: 100%;">
<img align="center" height="30" width="100" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/MongoDB_Logo.svg/2560px-MongoDB_Logo.svg.png" style="max-width: 100%;">
<img align="center" height="30" width="30" src="https://ps.w.org/jwt-auth/assets/icon-256x256.png?rev=2298869" style="max-width: 100%;">
</div>



## Project Setup
```
npm install
```

### Compiles and hot-reloads for development
```
nodemon app.js
```

### CRUD para produtos
```
URL: https://crud-nodejs-teste-melvimjones.vercel.app/produtos
```



GET: 
```
REQ: /
RES: res.json(produtos)
```
POST:
```
REQ: req.body
________________________________________
EXEMPLO json:
    {
        "descricao": "nome do produto",
        "preco": "00",
        "imagem": "http://end_da_imagem.jpg"
    }
________________________________________
RES: res.json(prodSalvo)
```
DELETE:
```
REQ: id = req.query.id
________________________________________
EXEMPLO:
    id = id_do_produto
________________________________________
RES:  res.send("removido indice:" + id)
```

PUT:
```
REQ: id = req.query.id
     prod = req.body
________________________________________

EXEMPLO:  {
        "descricao": "Nome Alterado",
        "preco": "00",
        "imagem": "http://end_da_imagem_nova.jpg"
    }
________________________________________
RES: res.send("Alterado com sucesso: ")
```

### GERAR TOKEN
```
URL: 127.0.0.1:3000/auth/
```
Autenticador POST
```
REQ: nome:req.body.nome,
    senha:req.body.senha
________________________________________

EXEMPLO:  
{
    "nome": "joao",
    "senha":"123"
}
________________________________________
RES: res.send(token)
```
### VERIFICAR TOKEN
```
URL: 127.0.0.1:3000/verificar
```
Autenticador POST
```
REQ: req.body.token
________________________________________
RES: res.json(decoded)
```
