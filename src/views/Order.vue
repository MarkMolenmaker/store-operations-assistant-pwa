<template>
  <div class="order">
    <span class="mb-1">Bestelling aanmaken</span>
    <form id="order-details" @submit.prevent="share_order">
      <div id="required-customer">
        <input type="text" placeholder="Naam" name="customer-name" required class="mb-half" autocomplete="off">
        <div class="last-details">
          <input type="date" placeholder="Ophaal datum" name="pickup-date" class="width-full" autocomplete="off">
          <a @click="optional_details = true" v-if="!optional_details"><i class="icon fas fa-angle-down"/></a>
        </div>
      </div>
      <div id="optional-customer" class="details" v-if="optional_details">
        <input type="tel" placeholder="Telefoonnummer" name="telephone-number" class="width-full" autocomplete="off">
        <a @click="optional_details = false"><i class="icon fas fa-angle-up"/></a>
      </div>
      <HorizontalDivider class="mb-half" side_color="dark-gray" middle_color="dark-gray"/>
      <SearchProductInput @addOrderLine="add_product"/>
      <HorizontalDivider class="mt-half mb-half" side_color="dark-gray" middle_color="dark-gray"/>
      <span class="mb-1">Bestellijst</span>
      <span v-if="Object.keys(order_list).length < 1">Geen producten op bestellijst</span>
      <div v-else class="order-list">
        <OrderProductLine @remove-product="remove_product" v-for="order in order_list" v-bind:key="order.sku" :sku="order.sku" :title="order.title" :img="order.img"/>
        <button class="share-button mt-half noselect">Deel je bestelling</button>
      </div>
    </form>
  </div>
</template>

<script>
import HorizontalDivider from '@/components/HorizontalDivider'
import SearchProductInput from '@/components/SearchProductInput'
import OrderProductLine from '@/components/OrderProductLine'
export default {
  components: { OrderProductLine, HorizontalDivider, SearchProductInput },
  data () {
    return {
      optional_details: false,
      order_list: {}
    }
  },
  methods: {
    add_product (title, sku, img) {
      if (!(sku in this.order_list)) {
        this.order_list[sku] = {
          title: title,
          sku: sku,
          img: img
        }
      }
    },
    remove_product (sku) {
      delete this.order_list[sku]
    },
    async share_order () {
      // Variables
      const LINE_HEIGHT = 150
      const OFFSET = 10
      const FONT_SIZE = 20

      // Initialize Canvas and Context
      const canvas = document.createElement('canvas')
      canvas.height = Object.keys(this.order_list).length * LINE_HEIGHT
      canvas.width = 512

      // Default settings for Context
      const context = canvas.getContext('2d')
      context.textAlign = 'start'
      context.textBaseline = 'top'

      // White background
      context.fillStyle = 'white'
      context.fillRect(0, 0, canvas.width, canvas.height)

      const orders = this.order_list

      // Load the barcode font
      const f = new FontFace('Barcode', 'url(https://fonts.gstatic.com/s/librebarcode128/v24/cIfnMbdUsUoiW3O_hVviCwVjuLtXeK_H9AI.woff2)')
      f.load().then(async function () {
        // Ready to use the font in a canvas context
        document.fonts.add(f)
        let index = 0
        for (const sku in orders) {
          const image = new Image(LINE_HEIGHT, LINE_HEIGHT)
          image.crossOrigin = 'anonymous'

          // eslint-disable-next-line
          await new Promise(r => image.onload = r, image.src = orders[sku].img)

          // Draw image
          context.drawImage(image, 0, index * LINE_HEIGHT, LINE_HEIGHT, LINE_HEIGHT)

          // Write title
          context.fillStyle = 'black'
          context.font = `${FONT_SIZE}px Arial`
          context.fillText(orders[sku].title, LINE_HEIGHT + OFFSET, index * LINE_HEIGHT + OFFSET)

          // Write sku and amount
          context.fillStyle = 'dark_gray'
          context.font = `${FONT_SIZE - 5}px Arial`
          context.fillText(orders[sku].sku, LINE_HEIGHT + OFFSET, index * LINE_HEIGHT + OFFSET * 1.5 + FONT_SIZE)
          context.fillText('2 colli', LINE_HEIGHT + OFFSET, index * LINE_HEIGHT + OFFSET * 1.5 + FONT_SIZE * 2)

          // Write barcode
          context.fillStyle = 'black'
          context.font = `${FONT_SIZE + 30}px Barcode`
          context.fillText(`*${orders[sku].sku}`, LINE_HEIGHT + OFFSET, index * LINE_HEIGHT + OFFSET * 1.5 + FONT_SIZE * 3)

          index += 1
        }

        // Vue Social Sharing
        console.log(canvas.toDataURL('image/jpeg'))
      })
    }
  }
}
</script>

<style scoped>
  .order {
    display: flex;
    padding: 0 1em;
    flex-direction: column;
  }
  span { color: var(--dark-gray-color) }
  input {
    color: var(--black-color);
    padding: .5em;
  }
  .icon { font-size: 1.5em; margin-left: .7em; }
  #order-details {
    display: flex;
    flex-direction: column;
  }
  .details {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .5em;
  }
  .last-details {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .5em;
  }
  #required-customer {
    display: flex;
    flex-direction: column;
  }
  #optional-customer {

  }
  .share-button {
    width: 90%;
    height: 3em;
    background-color: var(--orange-color);
    color: var(--white-color);
    border-radius: .5em;
    border: none;
    position: fixed;
    margin: 0 auto;
    bottom: 1em;
  }
</style>
