<template>
  <div>
    <div>{{title}}</div>
    <div style="display: flex">
      <v-text-field
          v-model="currentRange[0]"
          :max="max"
          :min="min"
          class="pa-0 mr-3"
          dense
          outlined
          hide-details
          type="number"
          style="width: 60px"
      />
      <v-text-field
          v-model="currentRange[1]"
          :max="max"
          :min="min"
          outlined
          dense
          class="pa-0 ma-0"
          hide-details
          type="number"
          style="width: 60px"
      />
    </div>
    <v-range-slider
        v-model="currentRange"
        :max="max"
        :min="min"
        hide-details
        class="align-center"
        color="green lighten-2"
    >
    </v-range-slider>
  </div>
</template>

<script>
export default {
  name: 'InputRange',

  model: {
    prop: 'range',
    event: 'change'
  },

  props: {
    title: {
      type: String,
      required: true
    },
    range: {
      type: Array,
      required: true
    },
    max: {
      type: Number,
      default: 100
    },
    min: {
      type: Number,
      default: 0
    }
  },

  computed: {
    currentRange: {
      get () {
        return this.range
      },
      set (newRange) {
        this.$emit('change', newRange)
      }
    }
  },
};
</script>
