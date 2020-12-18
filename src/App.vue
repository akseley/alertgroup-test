<template>
  <v-app>
    <v-app-bar app height="150">
      <v-container>
        <filters :disabled="loading" @applyFilters="applyFilters"/>
      </v-container>

    </v-app-bar>
    <v-main>
      <v-container>
        <v-layout v-if="!loading">
          <v-row class="mb-6">
            <v-col v-for="flat in flats" :key="flat.id" cols="3">
              <flat-card :flat="flat"/>
            </v-col>
          </v-row>
        </v-layout>
        <v-layout v-else column align-center>
          <v-progress-circular  indeterminate/>
        </v-layout>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Filters from "@/components/Filters";
import FlatCard from "@/components/FlatCard";

export default {
  name: 'App',

  components: {Filters, FlatCard},

  data: () => ({
    flats: [],
    loading: false,
  }),
  mounted() {
    this.getFlats()
  },
  methods: {
    applyFilters(filters) {
      this.filterData(filters)
    },
    async getFlats() {
      try {
        this.loading = true
        this.flats = await new Promise((resolve) => {
          setTimeout(() => {
            resolve(FLATS_DATA)
          }, 1000)
        })
      } finally {
        this.loading = false
      }


    },
    async filterData(filters) {
      try {
        this.loading = true

        this.flats = await new Promise((resolve) => {
          setTimeout(() => {
            const result = FLATS_DATA.filter(flat => this.getConditionFilter(flat, filters))
            resolve(result)
          }, 1000)
        })
      } finally {
        this.loading = false
      }
    },
    getConditionFilter(flat, filters) {
      return !Object.entries(filters).some(([key, value]) => {
        if (key === 'price') {
          return !this.filterRange(flat[key] / 1000000, value)
        } else if (Array.isArray(value)) {
          return !this.filterRange(flat[key], value)
        } else {
          return !this.filterString(flat[key], value)
        }
      })
    },
    filterString(element, value) {
      if (!value) {
        return true
      }
      return element === value
    },
    filterRange(element, [min, max]) {
      return element <= max && element >= min
    }
  }
};

const FLATS_DATA = [
  {
    building_id: 73,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 23329,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2956317,
    rooms: 1,
    size: "XS",
    square: 23.66,
  },
  {
    building_id: 74,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 20822,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2992701,
    rooms: 1,
    size: "XS",
    square: 23.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 20382,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 4952721,
    rooms: 2,
    size: "2k",
    square: 42.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 203321,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 8862732,
    rooms: 3,
    size: "3k",
    square: 42.87,
  },
  {
    building_id: 32,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 203282,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "1k",
    square: 24.99,
  },
  {
    building_id: 37,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 20320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "XS",
    square: 24.99,
  },
  {
    building_id: 17,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 5956317,
    rooms: 1,
    size: "2k",
    square: 45.36,
  },
  {
    building_id: 87,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 9956317,
    rooms: 4,
    size: "4",
    square: 66.60,
  },
  {
    building_id: 73,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 233291,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2956317,
    rooms: 1,
    size: "XS",
    square: 23.66,
  },
  {
    building_id: 74,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 208221,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2992701,
    rooms: 1,
    size: "XS",
    square: 23.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 203821,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 4952721,
    rooms: 2,
    size: "2k",
    square: 42.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 203322,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 8862732,
    rooms: 3,
    size: "3k",
    square: 42.87,
  },
  {
    building_id: 32,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 203283,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "1k",
    square: 24.99,
  },
  {
    building_id: 37,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 20320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "XS",
    square: 24.99,
  },
  {
    building_id: 17,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 5956317,
    rooms: 1,
    size: "2k",
    square: 45.36,
  },
  {
    building_id: 87,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 9956317,
    rooms: 4,
    size: "4",
    square: 66.60,
  },
  {
    building_id: 73,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 233292,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2956317,
    rooms: 1,
    size: "XS",
    square: 23.66,
  },
  {
    building_id: 74,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 208222,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2992701,
    rooms: 1,
    size: "XS",
    square: 23.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 203822,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 4952721,
    rooms: 2,
    size: "2k",
    square: 42.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 203323,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 8862732,
    rooms: 3,
    size: "3k",
    square: 42.87,
  },
  {
    building_id: 32,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 203284,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "1k",
    square: 24.99,
  },
  {
    building_id: 37,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 20320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "XS",
    square: 24.99,
  },
  {
    building_id: 17,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 5956317,
    rooms: 1,
    size: "2k",
    square: 45.36,
  },
  {
    building_id: 87,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 9956317,
    rooms: 4,
    size: "4",
    square: 66.60,
  },
  {
    building_id: 73,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 233293,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2956317,
    rooms: 1,
    size: "XS",
    square: 23.66,
  },
  {
    building_id: 74,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 208223,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 2992701,
    rooms: 1,
    size: "XS",
    square: 23.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 203823,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 4952721,
    rooms: 2,
    size: "2k",
    square: 42.87,
  },
  {
    building_id: 75,
    building_name: "1 этап 1а корпуса",
    floor: 4,
    id: 203324,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 8862732,
    rooms: 3,
    size: "3k",
    square: 42.87,
  },
  {
    building_id: 32,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 203281,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "1k",
    square: 24.99,
  },
  {
    building_id: 37,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 20320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 3956317,
    rooms: 1,
    size: "XS",
    square: 24.99,
  },
  {
    building_id: 17,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 5956317,
    rooms: 1,
    size: "2k",
    square: 45.36,
  },
  {
    building_id: 87,
    building_name: "1 этап 1а корпуса",
    floor: 10,
    id: 33320,
    is_studio: 1,
    number: "163",
    plan: "/img/bb8d/9eeb90d9c7aeeed41fb41c0b5e383013.jpg",
    porch: 3,
    price: 9956317,
    rooms: 4,
    size: "4",
    square: 66.60,
  },
]
</script>
