<template>
  <form action="#" class="comment-form" @submit.prevent="submit">
    <h2 class="form-title">Залишити оцінку та відгук</h2>
    <div class="form-content">
      <div class="form-control">
        <label for="name" class="input-label"
          >Представтесь:<span class="required" v-if="!anonymous">*</span></label
        >
        <input
          v-model.trim="formValues.name"
          type="text"
          name="name"
          id="name"
          placeholder="Вкажіть ваше прізвище та ім'я"
          class="input-field"
          autocomplete="off"
          maxlength="50"
          :disabled="anonymous"
          :required="!anonymous"
        />
        <label class="checkbox-field">
          <input
            type="checkbox"
            name="anonymous"
            id="anonymous"
            value="false"
            class=""
            v-model="anonymous"
          />
          <span>Анонімно</span>
        </label>
      </div>

      <div class="form-control">
        <div class="input-label">Оцініть роботу лікаря:<span class="required">*</span></div>
        <star-rating
          name="rating"
          @change-rating="changeRating"
          :currentRating="formValues.rating"
          :ratingRange="[
            { v: 1, label: 'Дуже погано', id: '6' },
            { v: 2, label: 'Погано', id: '7' },
            { v: 3, label: 'Нормально', id: '8' },
            { v: 4, label: 'Добре', id: '9' },
            { v: 5, label: 'Дуже добре', id: '10' },
          ]"
        />
      </div>

      <div class="form-control">
        <label for="comment" class="input-label">Напишіть відгук:</label>
        <textarea
          v-model.trim="formValues.comment"
          name="comment"
          id="comment"
          placeholder="Вкажіть відгук до 500 символів..."
          class="textarea"
          maxlength="500"
        />
      </div>
      <div class="form-buttons">
        <MyButton
          type="button"
          class="btn btn-secondary"
          @click="resetForm"
          :disabled="isFormEmpty"
        >
          Очистити
        </MyButton>
        <MyButton type="submit" class="btn btn-primary" :disabled="isFormValid">Надіслати</MyButton>
      </div>
    </div>
  </form>
</template>

<script>
import { reactive, ref, watch } from 'vue';
import StarRating from './StarRating.vue';
export default {
  name: 'CommentForm',
  components: {
    StarRating,
  },
  props: {
    closeModal: {
      type: Function,
    },
    addComment: {
      type: Function,
    },
  },
  setup(p) {
    const formValues = reactive({
      name: '',
      rating: 0,
      comment: '',
    });
    const anonymous = ref(false);
    const isFormEmpty = ref(true);
    const isFormValid = ref(true);

    const submit = () => {
      if (anonymous.value) formValues.name = '';

      p.addComment(formValues);

      resetForm();
      p.closeModal();
    };

    const resetForm = () => {
      formValues.name = '';
      formValues.rating = 0;
      formValues.comment = '';
      anonymous.value = false;
    };

    const changeRating = (value) => {
      formValues.rating = value;
    };

    const checkIsFormEmpty = ([formValues, anonymous]) => {
      return !(Object.values(formValues).some(Boolean) || anonymous);
    };

    const checkIsFormValid = ([formValues, anonymous]) => {
      return (
        (!anonymous && !formValues.name) ||
        formValues.name > 50 ||
        !formValues.rating ||
        formValues.comment.length > 500
      );
    };

    watch([formValues, anonymous], (v) => {
      isFormEmpty.value = checkIsFormEmpty(v);
      isFormValid.value = checkIsFormValid(v);
    });

    return { submit, formValues, anonymous, changeRating, resetForm, isFormEmpty, isFormValid };
  },
};
</script>

<style lang="scss" scoped>
.comment-form {
  padding: 20px;
}

.form-title {
  font-size: 28px;
  margin-bottom: 10px;
  color: blue;
  text-align: center;
  margin-bottom: 20px;
}

.form-control {
  display: flex;
  column-gap: 8px;

  &:not(:last-child) {
    margin-bottom: 30px;
  }
}

.input-label {
  flex: 0 0 30%;
  font-weight: 700;
}

.input-field {
  flex: 1;
  padding: 8px 12px;
  font: inherit;

  &:disabled {
    cursor: not-allowed;
  }
}

.required {
  color: red;
}

.checkbox-field {
  display: flex;
  flex-direction: column;
}

.textarea {
  resize: vertical;
  width: 100%;
  min-height: 100px;
  max-height: 250px;
  padding: 8px;
  font: inherit;
}

.form-buttons {
  display: flex;
  justify-content: flex-end;
  column-gap: 20px;
}
</style>
