<template>
  <div class="star-rating" :class="{ disabled: disabled }">
    <template v-for="{ v, label, id } in rr" :key="id">
      <input
        @change="onChange"
        :id="`star${id}`"
        :value="v"
        :disabled="disabled"
        :checked="v == currentRating"
        type="radio"
        name="rating"
        class="visually-hidden"
        :required="required"
      />
      <label :for="`star${id}`" class="rating-label"
        ><span class="star-symbol">★</span>
        <span class="label-text" v-if="label">{{ label }}</span>
      </label>
    </template>
  </div>
</template>

<script>
import { computed } from 'vue';
export default {
  name: 'StarRating',
  props: {
    name: {
      type: String,
    },
    required: Boolean,
    disabled: {
      type: Boolean,
      default: false,
    },
    currentRating: {
      type: Number,
    },
    ratingRange: {
      type: Array,
    },
  },
  emits: ['change-rating'],
  setup(props, ctx) {
    const onChange = (e) => {
      ctx.emit('change-rating', parseInt(e.target.value));
    };

    const rr = computed(() => [...props.ratingRange].reverse());

    return { onChange, rr };
  },
};
</script>

<style scoped>
.star-rating {
  display: flex;
  flex-direction: row-reverse;
  justify-content: space-around;
  column-gap: 10px;
}

.rating-labels {
  display: flex;
  column-gap: 10px;
}

.rating-label {
  display: block;
  text-align: center;
}

.rating-label .label-text {
  color: blue;
}

.star-symbol {
  display: block;
  font-size: 34px;
}

.star-symbol:not(:last-child) {
  margin-bottom: 4px;
}
.label-text {
  display: block;
  font-size: 12px;
  white-space: nowrap;
}

.star-rating > input:checked ~ label,
.star-rating:not(.disabled) > label:hover,
.star-rating:not(.disabled) > label:hover ~ label {
  color: #ffd700;
}

.star-rating:not(.disabled) > input:checked + label:hover,
.star-rating:not(.disabled) > input:checked ~ label:hover,
.star-rating:not(.disabled) > label:hover ~ input:checked ~ label,
.star-rating:not(.disabled) > input:checked ~ label:hover ~ label {
  color: #ffed85;
}
</style>
