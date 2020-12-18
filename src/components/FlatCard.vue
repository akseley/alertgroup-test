<template>
  <div>
    <v-card class="card rounded-lg">
      <div class="card-container">
          <div class="card-title text-body-2">
            <div class="grey--text font-weight-bold">{{flat.floor}} этаж</div>
            <div class="font-weight-bold">{{`${flat.rooms} комната - ${flat.square} м`}} <sup>2</sup></div>
          </div>
          <div class="card-img">
            <v-img class="rounded-lg border" :src="img"/>
            <div class="card-number font-weight-bold rounded-bl-lg">{{flat.number}}</div>
          </div>
          <div class="card-price">
            <div class="text-h6 font-weight-bold">{{ formatPrice(flat.price) }}р.</div>
            <div class="card-subprice grey--text caption">{{ calcPerMeter() }}р. за м<sup>2</sup></div>
          </div>
          <div class="card-actions">
          <v-btn color="green lighten-2 white--text" block>Подробнее</v-btn>
          </div>
      </div>
    </v-card>
  </div>
</template>

<script>
import img from '@/assets/flat_img.jpg'

export default {
  name: 'FlatCard',
  props: {
    flat: {
      type: Object,
      required: true
    }
  },
  computed: {
    img() {
      return this.flat.image ?? img
    }
  },
  methods: {
    formatPrice(price) {
      return (price).toLocaleString('ru-RU')
    },
    calcPerMeter() {
      const result = Math.floor(this.flat.price / this.flat.square)
      return this.formatPrice(result)
    }
  }
};
</script>
<style scoped lang="scss">
.card {
  &-container {
    padding: 16px;
    overflow: hidden;
  }
  &-img{
    position: relative;
    margin-bottom: 16px;
  }
  &-number{
    position: absolute;
    z-index: 2;
    top: 0;
    right: 0;
    padding: 5px 8px;
    border-left: 1px solid #ebebeb;
    border-bottom: 1px solid #ebebeb;
    border-bottom-left-radius: 5px;
  }
  &-title{
    display: flex;
    justify-content: space-between;
    padding-bottom: 16px;
  }
  &-price {
    padding-bottom: 16px;
    text-align: end;
  }
  &-subprice {
    text-align: end;
  }
}
.border {
  border: 1px solid #ebebeb ;
}
</style>
