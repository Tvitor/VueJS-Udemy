---
description: Anotações feitas durante as Aulas de VueJS - 
---

# VueJS

### Diretivas

> Diretivas são atributos especial pré fixados com v-

#### Diretiva V-bind

> v-bind, ao passar o atributo como parametro, o v-bind irá fazer uma ligação de databind. Fazendo o vueJS passar a monitorar esse elemento

#### v-bind:href

>fornecer link dinâmico para o DOM pelo href recebendo dados de propriedades de um objeto
> v-bind:atributo=variavel

```text
<a v-bind:href=docs>VueJS</a>
```

#### v-text: 

> com v-text permite por meio de strings exibir valores guardados em propriedades de objetos
```text
<p>Instrutor: <span v-text="instrutor"></span> </p>
```

#### v-once:
> Essa diretiva não espera valor na expressão, sendo apena v-once
> esse elemento e todos os filhos desse elemento será realizado somente 1 vez. Na próxima renderização será considerado conteúdo estático

```text
<p v-once>Nome Inteiro {{nome}}</p>
```
#### v-html
> permite interpretar código html contido em uma propriedade de um objeto
> 
```text
<p v-html="curso"> </p>
```
## Eventos
> com a diretiva v-on é possível capturar um evento e utiliza-lo com a propriedade de um objeto, chamando um metodo
> Também é possível capturar eventos com @
```text
        <button v-on:click="incrementar">Clique</button> // chama  o metodo incrementar
        <button @click="incrementar">Clique</button>
```

#### .stop
> utilizando o .stop no click, não permitirá que o evento seja propagado para toda a arvore do DOM , mantendo a captura do evento somente nessa linha

#### .prevent
> Utilizando  o .prevent default, executa  o método sem que atualize a página

#### v-on
> utilizado para capturar eventos de como cliques e teclas do teclado

```text
v-on:keyup="">
```

#### Computed
> propriedade que permite utilizar dados computados.

```text

<span>{{data}} => {{dadoInvertido}}</span>
computed:{
    dadoInvertido: function() {
        return this.data.split('').reverse().join('')
    }
}

```

#### Computed X Method

> Computed são cacheadas a partir de suas dependências (como em data). Com isso pode ser acessado em cache em momentos diferentes caso ele seja alterado. Somente será executado quando é alterado o dado desse dado. Ganhando em performance.
> Method é chamado em cada nova reenderização, mesmo que outra propriedade for alterada esse metodo será executado. 

#### Watch
> Alternativa a Computed. Utilizado quando for necessário executar operação assincrona ou quando não precisar retornar valor
> ex: Acessar uma API ou reagir a alteração de outros dados e executar uma operação assíncrona.

```text
data:{
                nomeCompleto: 'Joao Paulo'
            },
           watch: {
            nomeCompleto: function (novoNomeCompleto, antigoNomeCompleto) {
                let self = this;
                setTimeout(function() {
                    self.nomeCompleto = 'Nome resetado';
                },3000);
            }
           }

```
#### Computed com setter e getter
> com o get e set é possível setar um valor para a propriedade computed através de uma função

```text
computed: {
    nomeCompleto:{
        get: function(){
            return this.primeiroNome + ' ' + this.ultimoNome
        },
        set: function(novoNome) {
            let nomes = novoNome.split(' ');
            this.primeiroNome = nomes[0];
            this.ultimoNome = nomes[nomes.length -1];
        }
    }
}
```

#### Two way Databinds
> input para imprimir um valor e/ou retornar valor dinâmicamente

```text
<input :value="nome" @inpu="nome = $event.target.value">
    ou
<input: v-model="nome">
<script type="text/javascript>
 new Vuew({
     el: '#app',
     data: {
         nome: 'John'
     }
 })
</script>
```

## Manipulação Dinâmica de Css com dataBinds

```text
<style>
    .caixa{
        width: 200px;
        heigh: 200px;
        display: inline-block;
        margin-righ: 10px;
        background-color: gray;
    }
    .coral-a {
        background-color:lightcoral;
    }
</style>

<div id="app">
    <div 
        class="caixa"
        :class={'coral-a':true }
        @click="aplicarClasse = !aplicarClasse">
    </div>
</div>

<script type="text"/javascript">

    new Vue({
        el:'#app',
        data: {
            aplicarClasse: false
        }
    });
</script>

```

## Manipulação Dinâmica de styles com dataBinds

```text

<style>
    .caixa{
        width: 200px;
        heigh: 200px;
        display: inline-block;
        margin-righ: 10px;
        background-color: gray;
    }
    .coral-a {
        background-color:lightcoral;
    }
</style>

<div id="app">
    <div 
        class="caixa"
        :class={'coral-a':aplicarClasse }
        @click="aplicarClasse = !aplicarClasse">
    </div>
    <div>
        class="caixa"
        :class="nomeDaClasse">
    </div>
    <input v-model="nomedaClasse" placeholder="Nome da Calsse CSS">
</div>

<script type="text"/javascript">

    new Vue({
        el:'#app',
        data: {
            aplicarClasse: false,
            nomeDaClasse: ''
        }
    });
</script>

```

#### Estilizando CSS com Objetos

```text

<style>
    .caixa{
        width: 200px;
        heigh: 200px;
        display: inline-block;
        margin-righ: 10px;
        background-color: gray;
    }
    .coral-a {
        background-color:lightcoral;
    }
</style>

<div id="app">
    <div 
        class="caixa"
        :class={'coral-a':aplicarClasse }
        @click="aplicarClasse = !aplicarClasse">
    </div>
    <div>
        class="caixa"
        :class="nomeDaClasse">
    </div>
    <div
    class="caixa"
    :class="classesCSS">
    @click="aplicarClasse = !aplicarClasse">

    </div>
    <input v-model="nomedaClasse" placeholder="Nome da Calsse CSS">
</div>

<script type="text"/javascript">

    new Vue({
        el:'#app',
        data: {
            aplicarClasse: false,
            nomeDaClasse: ''
        },
        computed: {
            classesCSS: function(){
                return {
                    azul: this.aplicarClasse,
                    circulo: this.aplicarClasse,
                    verde: !this.aplicarClasse
                };
            }
        }
    });
</script>

```

#### Condição com V-if

```text

v-if="mostrar">
<button @click="mostrar = !mostrar">

data:{
    mostrar:true
}

```

#### Condição com V-else-if

```text
<v-if "nota === 'A'"> passou<>
<v-else-if "nota === 'B' ">não passou <>
<v-else "nota === 'C'>reprovado<>

v-model="nota" placeholder="Nota">


data:{
    nota:''
}

```

#### Condição com template

```text
<template v-if "nota === 'A'">
<li>1<>
<li>2<>
</template>

data:{
    nota:''
}

```

#### Controlando a reutilizaçãode elementos cmo KEY

```text
<button @click="login =!login">toggle</>
<template v-if="login">
<input placeholoder= "Login" key="campo-login">
</template>

<template v-else>
<input placeholoder= "Email" key="campo-email">

</template>
data:{
    login:true
}

```

#### Renderizando com v-for

```text

<ul>
    <li v-for="(produto, indice) in produtos">{{indice}} - {{produto}}</li>
<ul>

<ul>
    <li v-for="(valor, indice) in 30">{{indice}} - {{valor}}</li>
<ul>

data:{
    produtos: ['monitor', 'teclado', mouse]
}

```


#### Renderizando com v-for com objeto

```text

<ul>
    <li v-for="(valor, chave) in produtos" :key="valor.id">{{chave}} - {{valor.nome}}</li>
<ul>
        <!-- <button @click="addProduto">Inserir Produto</button> -->
        <button @click="produtos.reverse()">inverter Produto</button>
        <input v-model="novoProduto" placeholder="Novo Produto"></input>
        <input v-on:keyup.enter="addProduto" placeholder="Novo Produto"></input>

    </div>

    <script  type="text/javascript">

        new Vue({
	        el:'#app',
            data:{
                produtos: [
                    {id:1, nome:'pera'},
                    {id:2, nome:'uva'},
                ],
                novoProduto: ''
            },
            methods: {
                addProduto: function(event) {
                    this.novoProduto = event.target.value
                    console.log(event.target.value)
                    let id = this.produtos.length + 1;
                    this.produtos.push({id:id, nome: this.novoProduto});
                }
            }
        });

```

#### Diretivas v-for v-if e filtragem de arrays

```text

    <div id="app">
        <ul>
            <li v-for="(valor, chave) in tarefas" :key="valor.id" >{{chave}} - {{valor.titulo}}</li>
        </ul>
<h3>tarefas a fazer</h3>
        <ul>
            <li v-for="(valor, chave) in tarefasIncompletas" :key="valor.id" >{{chave}} - {{valor.titulo}}</li>
        </ul>
    </div>
            <script  type="text/javascript">
                new Vue({
                    el:'#app',
                    data:{
                        tarefas: [
                            {id:1, titulo:'java', completa: true},
                            {id:2, titulo:'nodejs', completa: false},
                        ]
                    },
                    computed: {
                        tarefasIncompletas: function() {
                            return this.tarefas.filter(function(tarefa){
                                return !tarefa.completa;
                            })
                        }
                    }
                });
    </script>

```
#### Detectando mudanças em arrays

```text

        <ul>
            <li v-for="(valor, chave) in produtos" :key="valor.id" >{{chave}} - {{valor.titulo}}</li>
        </ul>
        <button @click="adicionarProduto">Adicionar produto</button>
        <button @click="produtos = produtos.slice(0,4)">Substituir produto</button>
        <button @click="substituirProduto">substituirProduto</button>
        <button @click="cortarArray">Cortar</button>
    </div>
            <script  type="text/javascript">
                new Vue({
                    el:'#app',
                    data:{
                        produtos: [
                            {id:1, titulo:'monitor'},
                            {id:2, titulo:'teclado'},
                            {id:3, titulo:'mouse'},
                            {id:4, titulo:'processador'},

                        ]
                    },
                    methods: {
                        adicionarProduto: function(event) {
                            let id = this.produtos.length + 1;
                            this.produtos.push({id: id, titulo:'Produto'})
                        },
                        substituirProduto: function(event){
                            let tamanho = this.produtos.length;
                            let indice = Math.round(tamanho / 2);
                            let novoProduto = {id: (tamanho + 1), nome: 'Produto'}
                            this.produtos.splice(indice, 1, novoProduto);
                        },
                        cortarArray: function(event) {
                            this.produtos.splice(2);
                        }
                    }
                });

```

#### Detectando mudanças em objetos

```text

<ul>
    <li v-for="(valor, chave) in produtos" :key="valor.id" >{{chave}} - {{valor}}</li>
</ul>
    <button @click="adicionarPropriedade">adicionarPropriedade</button>
    <button @click="substituirObjeto">substituirObjeto</button>
</div>
    <script  type="text/javascript">
        new Vue({
            el:'#app',
            data:{
                produtos: 
                    {id:1, titulo:'monitor'}
            },
            usuario: {
                nome: '',
                idade: 0
            },
            methods: {
                adicionarPropriedade: function(event) {
                    Vue.set(this.produtos, 'preco', 100)
                },
                substituirObjeto: function(event) {
                    this.produtos = Object.assign({},this.produtos, {
                        preco:50,
                        cor:'preta'
                    });
                }
            }
        });

```

