<template>
  <header>
    <!-- 네비 -->
    <nav class="menu">
      <a v-for="(navItem, idx) in navList" :key="idx" :href="navItem.path">
        {{ navItem.name }}
      </a>
    </nav>
  </header>

  <main>
    <div class="container">
      <!-- 할인 -->
      <Discount v-if="isDiscount" />

      <!-- 정렬 -->
      <button @click="sortProducts('name')">이름순</button>
      <button @click="sortProducts('asc')">낮은 가격순</button>
      <button @click="sortProducts('desc')">높은 가격순</button>
      <button @click="sortProducts('init')">되돌리기</button>
  
      <!-- 상품 리스트 -->
      <div class="content">
        <Card v-for="product in products" :key="product.id" :product="product" @openModal="openModal($event)" />
      </div>
    </div>
  </main>

  <!-- 모달 -->
  <Transition name="fade">
    <Modal v-if="isModalOpen" :product="products[modalId]" :isDiscount="isDiscount" @closeModal="closeModal" />
  </Transition>
</template>

<script>
  import './assets/common.css';
  import data from './data/products';
  import Modal from './components/Modal.vue';
  import Discount from './components/Discount.vue';
  import Card from './components/Card.vue';

  export default {
    name: 'App',
    data() {
      return {
        modalId: 0,
        isModalOpen: false,
        isDiscount: true,
        navList: [
          {
            name: 'Home',
            path: '/'
          },
          {
            name: 'Shop',
            path: '/shop'
          },
          {
            name: 'About',
            path: '/about'
          }
        ],
        products: data,
        initProducts: [...data],
      }
    },
    methods: {
      openModal(id) {
        this.isModalOpen = true;
        this.modalId = id;
      },
      closeModal() {
        this.isModalOpen = false;
      },
      sortProducts(type) {
        const sortMethods = {
          init: () => {
            this.products = [...this.initProducts];
          },
          name: () => {
            this.products.sort((a, b) => {
              const nameA = a.title.toUpperCase();
              const nameB = b.title.toUpperCase();

              if (nameA < nameB) {
                return -1;
              } 
              else if (nameA > nameB) {
                return 1;
              } 
              else {
                return 0;
              }
            });
          },
          asc: () => {
            this.products.sort((a, b) => a.price - b.price);
          },
          desc: () => {
            this.products.sort((a, b) => b.price - a.price);
          }
        };

        sortMethods[type]()
      }
    },
    components: {
      Discount,
      Modal,
      Card
    }
  }
</script>

<style>
  .menu {
    background: darkslateblue;
    padding: 15px;
    margin-bottom: 30px;
  }

  .menu a {
    color: white;
    padding: 10px;
    text-decoration: none;
    transition: all .3s;
  }

  .menu a:hover {
    opacity: .7;
  }

  .container {
    max-width: 1440px;
    margin: 0 auto;
  }

  .content {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }

  .room-img {
    width: 100%;
  }

  /* start transition */
  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-active {
    transition: all .3s;
  }
  .fade-enter-to {
    opacity: 1;
  }

  /* end transition */
  .fade-leave-from {
    opacity: 1;
  }
  .fade-leave-active {
    transition: all .3s;
  }
  .fade-leave-to {
    opacity: 0;
  }
</style>