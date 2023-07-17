<template>
  <div class="modal">
    <div class="modal-container">
      <div class="modal-header">
        <h4>{{ product.title }}</h4>
        <button @click="closeModal" class="modal-close-btn">
          <i class="line"></i>
          <i class="line"></i>
        </button>
      </div>
      <div class="modal-body">
        <div>
          <Discount v-if="isDiscount" />
          <img class="room-img" :src="product.image" alt="room">
          <div>
            <!-- <input :value="month" @input="month = $event.target.value" type="number" min="1" max="12" placeholder="개월 수 입력"> -->
            <input v-model.number="month" type="number" min="1" max="12" placeholder="개월 수 입력">
          </div>
          <p>{{ month }}개월 합계 : {{ (product.price * month).toLocaleString('ko-KR') }}원</p>
          <p>{{ product.content }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Discount from './Discount.vue';
  export default {
    name: 'Modal',
    data() {
      return {
        month: 1,
      }
    },
    props: {
      product: Object,
      isDiscount: Boolean,
    },
    methods: {
      closeModal() {
        this.$emit('closeModal');
      }
    },
    components: {
      Discount,
    }
  }
</script>

<style>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .5);
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal-container {
    width: 100%;
    max-width: 1200px;
    height: fit-content;
    max-height: 100%;
    background: white;
    border-radius: 10px;
    padding: 20px;  
    display: flex;
    flex-direction: column;
    gap: 30px 0;
  }

  .modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
    flex-shrink: 0;
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
    cursor: pointer;
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

  .modal-body {
    flex-grow: 1;
    overflow: auto;
  }
</style>