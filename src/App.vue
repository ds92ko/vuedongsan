<template>
  <nav class="menu">
    <a v-for="(navItem, idx) in navList" :key="idx">{{ navItem }}</a>
  </nav>
  <div v-for="(product, idx) in products" :key="idx">
    <h4>{{ product.name }}</h4>
    <p>{{ product.price }}만원</p>
    <button @click="increase(idx)">허위매물신고</button> <span>신고 횟수: {{ product.reportNum }}</span>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      navList: ['Home', 'Shop', 'About'],
      products: [
        {
          name: '역삼동원룸',
          price: 50,
          reportNum: 0
        },
        {
          name: '천호동원룸',
          price: 60,
          reportNum: 0
        },
        {
          name: '마포구원룸',
          price: 70,
          reportNum: 0
        },
      ]
    }
  },
  methods: {
    increase(idx) {
      this.products[idx].reportNum++;
    }
  },
  components: {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}
</style>
