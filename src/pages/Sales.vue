<style lang="stylus">
  .grid-container {
    display: grid
    grid-template-columns: 1fr 1fr 1fr
    grid-template-rows: auto
    grid-template-areas:
      "item item receipt"
  }

  .item-to-choose-area {
    grid-area: item
  }

  .receipt-area {
    grid-area: receipt
  }

</style>

<template>
  <q-page class="grid-container">
    <div class="item-to-choose-area">
      <div class="row">
        <template v-for="(product, i) in products">
          <div class="col-2 shadow-1 q-ma-sm" :key="`product${i}`"
              @click="doSelectAProduct(product)">
            <q-card inline class="q-ma-sm">
              <q-card-media>
                <img :src="url" width="100" height="100">
                <q-card-title slot="overlay">
                  <span slot="subtitle">{{product.name}} {{(product.price).toFixed(2)}}</span>
                </q-card-title>
              </q-card-media>
            </q-card>
          </div>
        </template>
      </div>
    </div>
    <div class="receipt-area shadow-1">
      <q-list>
        <q-item v-for="(receipt, i) in receipts" :key="`receipt${i}`">
          <q-item-side left><div @click="doRemoveThisItem(i)">x</div></q-item-side>
          <q-item-main :label="receipt.name" />
          <q-item-side right>{{(receipt.price).toFixed(2)}}</q-item-side>
        </q-item>
      </q-list>
      <div class="flex flex-center q-mt-sm">
        <span class="q-title text-black">CHARGE {{(totalAmount).toFixed(2)}}</span>
      </div>
      <div class="flex flex-center q-mt-sm">
        <q-btn @click="doClearAllTransaction" >CLEAR</q-btn>
        <q-btn @click="doPay" >PAY</q-btn>
      </div>
    </div>

  </q-page>
</template>
<script>
export default {
  name: 'Sales',
  data () {
    return {
      url: 'data:image/jpeg;base64,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',
      products: [
        { name: 'V-nec Dress', url: '', price: 55.0 },
        { name: 'Geo Dress', url: '', price: 100.0 },
        { name: 'A-line Dress', url: '', price: 45.0 },
        { name: 'Woven Dress', url: '', price: 10.0 },
        { name: 'Grey Dress', url: '', price: 25.0 },
        { name: 'Denim Dress', url: '', price: 30.0 },
        { name: 'Chambray Dress', url: '', price: 79.0 },

        { name: 'Cargo Dress', url: '', price: 102.0 },
        { name: 'Zip Jacket', url: '', price: 12.0 },
        { name: 'Jacket', url: '', price: 34.0 },
        { name: 'Bomber', url: '', price: 25.0 },

        { name: 'Khakis', url: '', price: 152.0 },
        { name: 'Dark Denim', url: '', price: 130.0 },
        { name: 'Cargo Jacket', url: '', price: 120.0 },
        { name: 'Sweatshirt', url: '', price: 110.0 },

        { name: 'Dotted Shirt', url: '', price: 130.0 },
        { name: 'Henley', url: '', price: 132.0 }
      ],
      receipts: [],
      total: 10
    }
  },
  computed: {
    totalAmount () {
      return this.receipts.reduce((sum, v) => (sum + v.price), 0)
    }
  },
  methods: {
    doSelectAProduct (product) {
      this.receipts.push(product)
    },
    doRemoveThisItem (i) {
      this.receipts.splice(i, 1)
    },
    doClearAllTransaction () {
      if (!this.receipts.length) return
      this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure you want to clear all?',
        ok: 'OK',
        cancel: 'Cancel'
      }).then(() => {
        this.receipts = []
      }).catch(() => {})
    },
    doPay () {
      if (!this.receipts.length) return
      // set to websocket

      const ws = new WebSocket('ws://demos.kaazing.com/echo')
      ws.onopen = () => {
        const payload = { event: 'purchase', amount: this.totalAmount }
        ws.send(JSON.stringify(payload))
      }

      ws.onmessage = (event) => {
        const resp = JSON.parse(event.data)
        // Confirm to the user that the payment has been processed.
        this.$q.dialog({
          title: 'Purchase',
          message: `Payment has been processed. ${(resp.amount).toFixed(2)}`
        }).then(() => {
          return this.$q.dialog({
            title: 'Receipt To Print',
            message: JSON.stringify(this.receipts, null, 2)
          })
        }).then(() => {
          // clear
          this.receipts = []
        }).catch(() => {})

        ws.close()
      }
    }
  }
}
</script>
