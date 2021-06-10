<template>
<section>
<!-- Modal -->
<div class="modal fade" ref="modal" id="userProductModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header bg-sgray">
        <h5 class="modal-title fw-bolder" id="userProductModal">{{ product.title }}</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <div class="row">
          <div class="col-6">
            <img :src="product.imageUrl" class="img-fluid" alt="product-pic" style="height: 230px;">
          </div>
          <div class="col-6">
            <p class="lh-lg mb-5">使用比利時嘉麗寶黑巧克力製作，濃郁的黑巧克力帶有苦甜的滋味，每咬一口都有滿滿的幸福感</p>
            <div>
              <p class="text-decoration-line-through">原價：NT$ 80</p>
              <p class="h4 fw-bolder">售價：NT$ 60</p>
            </div>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-hgray hvr-bounce-to-right">加入購物車</button>
      </div>
    </div>
  </div>
</div>
</section>
</template>
<script>
import * as bootstrap from 'bootstrap'

export default {
  // 從外層傳入變數 product，(擔心單一數據流的問題)預計使用 tempProduct 來接收
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
