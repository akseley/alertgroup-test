<template>
  <div>
    <v-row>
      <v-col>
        <div>Комнаты</div>
        <v-btn-toggle v-model="filters.size" color="green lighten-2">
          <v-btn v-for="size in sizeGroup" :key="size" :value="size">
            {{ size }}
          </v-btn>
        </v-btn-toggle>
      </v-col>
      <v-col>
        <input-range v-model="filters.floor" title="Этаж" :max="defaultFloorMax"/>
      </v-col>
      <v-col>
        <input-range v-model="filters.square" title="Площадь" :max="defaultSquareMax"/>
      </v-col>
      <v-col>
        <input-range v-model="filters.price" title="Цена" :max="defaultPriceMax"/>
      </v-col>
      <v-col>
        <v-btn class="mb-1 green lighten-2 white--text" :disabled="disabled" @click="apply">Применить</v-btn>
        <v-btn class="green lighten-2 white--text" :disabled="disabled" @click="reset">Сбросить фильтр</v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import InputRange from "@/components/InputRange";

const DEFAULT_MIN = 0
const DEFAULT_FLOOR_MAX = 100
const DEFAULT_SQUARE_MAX = 999
const DEFAULT_PRICE_MAX = 99

const DEFAULT_FILTERS = {
  size: '',
  floor: [DEFAULT_MIN, DEFAULT_FLOOR_MAX],
  square: [DEFAULT_MIN, DEFAULT_SQUARE_MAX],
  price: [DEFAULT_MIN, DEFAULT_PRICE_MAX],
}

export default {
  name: 'Filters',

  components: {InputRange},

  props: {
    disabled: {
      type: Boolean,
      default: false
    }
  },

  data: () => ({
    filters: JSON.parse(JSON.stringify(DEFAULT_FILTERS)),
    sizeGroup: ['XS','1k','2k','3k','4k'],
    defaultFloorMax: DEFAULT_FLOOR_MAX,
    defaultSquareMax: DEFAULT_SQUARE_MAX,
    defaultPriceMax: DEFAULT_PRICE_MAX,
  }),
  methods: {
    apply() {
      this.$emit('applyFilters', this.filters)
    },
    reset() {
      this.filters = JSON.parse(JSON.stringify(DEFAULT_FILTERS))
      this.$emit('applyFilters', this.filters)
    },
  }
};
</script>
