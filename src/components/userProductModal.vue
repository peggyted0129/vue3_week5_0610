<template>
<section>
<!-- Modal -->
<div class="modal fade" ref="modal" id="userProductModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="userProductModal">Modal title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
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
