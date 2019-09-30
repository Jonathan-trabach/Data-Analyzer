<template>
  <div>
   <!-- 
    <button class="btn btn-dark btn-block" v-if="!gridMontado" @click="getDados()">BUSCAR DADOS</button>
    <div class="container">
      <ProdutosItem
        v-for="produto in produtos"
        :key="produto.id"
        :item="produto"
      />
    </div>
    --> 
  </div>
</template>

<script>
import ProdutosItem from './ProdutosItem.vue'
export default {
  name: 'Search',
  components: {
    ProdutosItem
  },
  props: {
    msg: String
  },
  data() {
    return {
      dados: [],
      produtos: [],
      gridMontado: false,
     /*  page: Number, */
      search: []
    }
  },
  methods: {
    async getDados() {
      this.gridMontado = true
      const response = await fetch(
        'https://api.lomadee.com/v2/1501065109550272d9f6a/offer/_search?sourceId=35796574&keyword='  +
          this.search 
      )
      const json = await response.json()
      this.dados = json
      for (let index = 0; index < this.dados.offers.length; index++) {
        let element = this.dados.offers[index]
        this.produtos.push(element)
      }
      /* this.page = 0 */
    }
  },
  /* changePage(page) {
    if (this.page < 0) {
      this.page++
    }
    if (this.page * 15 + 15 > this.dados.length) {
      this.page--
    }
    this.page = this.page + page
    this.produtos = []
    for (let index = this.page * 15; index < this.page * 15 + 15; index++) {
      let element = this.dados[index]
      this.produtos.push(element)
    }
  }*/
} 
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  --color: #2c3e50;
  --margin-top: 60px;
  background : #eee;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}


</style>
