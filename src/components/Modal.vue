<template>
  <div class="modal">
    <div class="modal-container">
      <div class="modal-header">
        <h4>{{ product.title }}</h4>
        <button @click="$emit('closeModal')" class="modal-close-btn">
          <i class="line"></i>
          <i class="line"></i>
        </button>
      </div>
      <div class="modal-body">
        <div>
          <Discount v-if="isDiscount" />
          <img class="room-img" :src="product.image" alt="room">
          <div>
            <input v-model="month" placeholder="개월 수 입력">
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
    watch: {
      month(newValue, oldValue) {
        const max = 12;

        if (/\D/.test(newValue)) {
          alert('숫자만 입력 가능합니다.');
          this.month = 1;
          return;
        }
        if (!newValue) {
          this.month = 0;
          return;
        }
        if (oldValue === 0) {
          this.month = newValue.slice(1);
          return;
        }
        if (newValue > max) {
          alert('최대 12까지 입력 가능합니다.');
          this.month = oldValue;
          return;
        }
      }
    },
    props: {
      product: Object,
      isDiscount: Boolean,
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