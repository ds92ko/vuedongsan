<template>
  <div @click="() => openModal(product.id)" class="card">
    <img class="room-img" :src="product.image" alt="room">
    <h4>{{ product.title }}</h4>
    <p>{{ product.price.toLocaleString('ko-KR') }}원</p>
  </div>
</template>

<script>
  export default {
    name: 'Card',
    props: {
      product: Object,
      openModal: Function,
    }
  }
</script>

<style>
  .card {
    width: calc(50% - 10px);
    max-width: calc(1420px / 2);
  }

  @media all and (max-width: 768px) {
    .card {
      width: 100%;
    }
  }
</style>