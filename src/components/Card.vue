<template>
  <div class="card">
    <img class="room-img" :src="product.image" alt="room">
    <h4 @click="openModal">{{ product.title }}</h4>
    <p>{{ product.price.toLocaleString('ko-KR') }}원</p>
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props: {
      product: Object,
    },
    methods: {
      openModal() {
        this.$emit('openModal', this.product.id);
      }
    }
  }
</script>

<style>
  .card {
    width: calc(50% - 10px);
    max-width: calc(1420px / 2);
  }

  .card h4 {
    cursor: pointer;
  }

  @media all and (max-width: 768px) {
    .card {
      width: 100%;
    }
  }
</style>