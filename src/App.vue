<template>
  <!-- 모달 -->
  <div v-if="isModalOpen === true" class="modal">
    <div class="modal-content">
      <div class="modal-header">
        <h4>상세페이지임</h4>
        <button @click="closeModal" class="modal-close-btn">
          <i class="line"></i>
          <i class="line"></i>
        </button>
      </div>
      <div class="modal-body">
        <p>상세페이지 내용임</p>
      </div>
    </div>
  </div>

  <!-- 네비 -->
  <nav class="menu">
    <a v-for="(navItem, idx) in navList" :key="idx">{{ navItem }}</a>
  </nav>

  <!-- 상품 리스트 -->
  <div v-for="product in products" :key="product.id">
    <img class="room-img" :src="product.image" alt="room">
    <h4 @click="openModal">{{ product.title }}</h4>
    <p>{{ product.price }}만원</p>
  </div>
</template>

<script>
  import data from './data/products';

  export default {
    name: 'App',
    data() {
      return {
        isModalOpen: false,
        navList: ['Home', 'Shop', 'About'],
        products: data,
      }
    },
    methods: {
      openModal() {
        this.isModalOpen = true;
      },
      closeModal() {
        this.isModalOpen = false;
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

  body {
    margin: 0;
  }

  div {
    box-sizing: border-box;
  }

  .modal {
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .5);
    position: fixed;
    padding: 20px;
  }

  .modal-content {
    width: 100%;
    background: white;
    border-radius: 8px;
    padding: 20px;  
  }

  .modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
  }

  .modal-header h4 {
    margin: 0;
    flex-grow: 1;
  }

  .modal-close-btn {
    position: relative;
    background: none;
    border: 0;
    padding: 0;
    width: 30px;
    height: 30px;
  }

  .modal-close-btn .line {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) rotate(45deg);
    display: block;
    width: 100%;
    height: 2px;
    background: black;
  }

  .modal-close-btn .line:last-of-type {
    transform: translate(-50%, -50%) rotate(-45deg);
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

  .room-img {
    width: 100%;
    margin-top: 40px;
  }
</style>
