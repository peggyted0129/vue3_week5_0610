<template>
<section>
<!-- Modal -->
<div class="modal fade" ref="modal" id="userProductModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header bg-sgray">
        <h5 class="modal-title fw-bolder" id="userProductModal">{{ tempProduct.title }}</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body p-7">
        <div class="row">
          <div class="col-6">
            <img :src="tempProduct.imageUrl" class="img-fluid" alt="product-pic" style="height: 230px;">
          </div>
          <div class="col-6">
            <span class="badge bg-secondary mt-5 mb-3">{{ tempProduct.category }}</span>
            <p class="lh-lg mb-6">{{ tempProduct.content }}</p>
            <div class="mb-7">
              <p v-if="!tempProduct.price" class="text-decoration-line-through">{{ tempProduct.origin_price }}</p>
              <p v-if="tempProduct.price" class="text-decoration-line-through">原價：NT$ {{ tempProduct.origin_price }}</p>
              <p v-if="tempProduct.price" class="h4 fw-bolder">售價：NT$ {{ tempProduct.price }}</p>
            </div>
            <div class="input-group">
              <input type="number" v-model.number="qty" min="1" class="form-control">
              <button type="button" @click="$emit('add-cart', tempProduct.id, qty)" class="btn btn-hgray hvr-bounce-to-right">加入購物車</button>
            </div>
          </div>
        </div>
      </div>
      <!-- <div class="modal-footer">
        <button type="button" class="btn btn-hgray hvr-bounce-to-right">加入購物車</button>
      </div> -->
    </div>
  </div>
</div>
</section>
</template>
<script>
import * as bootstrap from 'bootstrap'

export default {
  // 從外層傳入變數 product，(擔心單一數據流的問題)預計使用 tempProduct 來接收
  // 如此一來，tempProduct 內容已和外層的 product 無關
  // 若要避免 "單向數據流" 的問題，盡量不要用外層傳入的資料
  props: ['product'],
  data () {
    return {
      status: {},
      modal: '',
      tempProduct: {},
      qty: 1
    }
  },
  watch: {
    product () {
      this.tempProduct = this.product
    }
  },
  methods: {
    openModal () {
      this.modal.show()
    },
    hideModal () {
      this.modal.hide()
    }
  },
  mounted () {
    this.modal = new bootstrap.Modal(this.$refs.modal, {
      keyboard: false,
      backdrop: 'static'
    })
  }
}
</script>
