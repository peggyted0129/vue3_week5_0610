<template>
<section class="py-20">
  <div class="container">
    <!--- 商品卡片 --->
    <div class="row mt-9">
      <div class="col-md-3 mb-7" v-for="item in products" :key="item.id">
        <a href="#" class="product-card" @click.prevent="openModal(item)">
          <div class="card position-relative back-card-shadow border-0 card-radius">
            <div style="height: 253px; background-size: contain; background-position: center; background-repeat: no-repeat;"
              :style="{backgroundImage: `url(${item.imageUrl})`}">
            </div>
            <div class="card-bg d-flex align-items-center">
              <p class="text-white fw-bolder p-8">{{ item.description }}</p>
            </div>
            <div class="card-body bg-light p-4" style="height: 100px">
              <div class="d-flex justify-content-between mb-3">
                <h5 class="card-title mb-0 text-theme fw-bolder">{{ item.title }}</h5>
                <span class="badge bg-secondary align-self-center">{{ item.category }}</span>
              </div>
              <div class="d-flex justify-content-between align-items-baseline">
                <div class="h5" v-if="!item.price">{{ item.origin_price }} 元</div>
                <del class="h6 text-streak" v-if="item.price">NT$ {{ item.origin_price }} 元</del>
                <div class="h5 text-danger fw-bolder" v-if="item.price">NT$ {{ item.price }} 元</div>
              </div>
            </div>
            <div class="card-footer position-relative bg-light d-flex align-items-center p-7">
              <button type="button" @click="addCart(item.id)" class="btn position-absolute start-0 zindex-1 border-end btn-product-card hvr-bounce-to-right py-2 px-0 w-50">
                <i class="fas fa-shopping-cart me-1"></i>
                加到購物車
              </button>
              <button type="button" class="btn position-absolute zindex-1 end-0 hvr-icon-wobble-vertical btn-product-card py-2 px-0 w-50">
                <i class="fas fa-file-alt hvr-icon me-1"></i>
                詳細資訊
              </button>
            </div>
          </div>
        </a>
      </div>
    </div>
  </div>
  <!-- Modal -->
  <user-product-modal ref="userProductModal" :product="product" @add-cart="addCart"></user-product-modal>
</section>
</template>
<script>
import userProductModal from '@/components/userProductModal.vue'

export default {
  components: {
    userProductModal
  },
  data () {
    return {
      products: [],
      product: {}
    }
  },
  methods: {
    getProducts () {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/products`
      vm.$http.get(api).then((res) => {
        console.log('產品 All 列表', res.data)
        if (res.data.success) {
          vm.products = res.data.products
        } else {
          vm.$swal({ title: res.data.message, icon: 'error' })
        }
      })
    },
    addCart (id, qty = 1) {
      const vm = this
      const cart = {
        product_id: id,
        qty
      }
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/cart`
      vm.$http.post(api, { data: cart }).then((res) => {
        console.log('加入購物車', res.data, cart)
        vm.$swal({ title: res.data.message, icon: 'success' })
      })
    },
    openModal (item) {
      const vm = this
      console.log(item)
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/product/${item.id}`
      vm.$http.get(api).then((res) => {
        vm.product = res.data.product
        vm.$refs.userProductModal.openModal()
      })
    }
  },
  created () {
    this.getProducts()
  }
}
</script>
