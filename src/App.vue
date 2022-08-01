<template>
  <div class="container">
    <h1 class="page-title">Профіль лікаря</h1>
    <div class="doctor-info">
      <div class="doctor-info-main">
        <h2 class="doctor-fullname">Тестова Оксана Василівна</h2>
        <StarRating
          :currentRating="rating"
          :disabled="true"
          :ratingRange="[
            { v: 1, id: '1' },
            { v: 2, id: '2' },
            { v: 3, id: '3' },
            { v: 4, id: '4' },
            { v: 5, id: '5' },
          ]"
        />

        <div class="avg-rating">(Середня оцінка: {{ rating }})</div>
      </div>
      <div class="doctor-info-other">
        <div class="doctor-photo">
          <img src="./assets/doctor-img1.jpg" alt="фото" />
        </div>
        <div class="info-block">
          <table class="info-table">
            <tr>
              <td><b>Місто:</b></td>
              <td>Львів</td>
            </tr>
            <tr>
              <td><b>Місце роботи:</b></td>
              <td>Львів, площа ринок, 10</td>
            </tr>
            <tr>
              <td><b>Заклад:</b></td>
              <td>
                <a href="#"
                  >Заклад Lorem ipsum dolor sit amet consectetur adipisicing elit. Harum,
                  suscipit.</a
                >
              </td>
            </tr>
          </table>
          <MyButton type="button" class="btn btn-primary leave-comment-btn" @click="openModal"
            >Залишити відгук</MyButton
          >
        </div>
      </div>
    </div>
    <CommentsList
      :comments="slicedComments"
      :loadMore="loadMore"
      :maxCommentsToShow="maxCommentsToShow"
      :maxComments="maxComments"
    />
  </div>

  <ModalRoot :isOpen="isModalOpen" @close="isModalOpen = false">
    <CommentForm :closeModal="closeModal" :addComment="addComment" />
  </ModalRoot>
</template>

<script>
import { computed, ref } from 'vue';

import StarRating from './components/StarRating.vue';
import ModalRoot from './components/ModalRoot.vue';
import CommentForm from './components/CommentForm.vue';
import CommentsList from './components/CommentsList.vue';

export default {
  name: 'App',
  components: {
    StarRating,
    ModalRoot,
    CommentForm,
    CommentsList,
  },
  setup() {
    const rating = ref(3);
    const isModalOpen = ref(false);

    const maxCommentsToShow = ref(5);
    const comments = ref([
      {
        id: 1,
        author: 'id labore ex et quam laborum',
        comment:
          'laudantium enim quasi est quidem magnam voluptate ipsam eos\ntempora quo necessitatibus\ndolor quam autem quasi\nreiciendis et nam sapiente accusantium',
      },
      {
        id: 2,
        author: 'quo vero reiciendis velit similique earum',
        comment:
          'est natus enim nihil est dolore omnis voluptatem numquam\net omnis occaecati quod ullam at\nvoluptatem error expedita pariatur\nnihil sint nostrum voluptatem reiciendis et',
      },
      {
        id: 3,
        author: 'odio adipisci rerum aut animi',
        comment:
          'quia molestiae reprehenderit quasi aspernatur\naut expedita occaecati aliquam eveniet laudantium\nomnis quibusdam delectus saepe quia accusamus maiores nam est\ncum et ducimus et vero voluptates excepturi deleniti ratione',
      },
      {
        id: 4,
        author: 'alias odio sit',
        comment:
          'non et atque\noccaecati deserunt quas accusantium unde odit nobis qui voluptatem\nquia voluptas consequuntur itaque dolor\net qui rerum deleniti ut occaecati',
      },
      {
        id: 5,
        author: 'vero eaque aliquid doloribus et culpa',
        comment:
          'harum non quasi et ratione\ntempore iure ex voluptates in ratione\nharum architecto fugit inventore cupiditate\nvoluptates magni quo et',
      },
      {
        id: 6,
        author: 'et fugit eligendi deleniti quidem qui sint nihil autem',
        comment:
          'doloribus at sed quis culpa deserunt consectetur qui praesentium\naccusamus fugiat dicta\nvoluptatem rerum ut voluptate autem\nvoluptatem repellendus aspernatur dolorem in',
      },
      {
        id: 7,
        author: 'repellat consequatur praesentium vel minus molestias voluptatum',
        comment:
          'maiores sed dolores similique labore et inventore et\nquasi temporibus esse sunt id et\neos voluptatem aliquam\naliquid ratione corporis molestiae mollitia quia et magnam dolor',
      },
      {
        id: 8,
        author: 'et omnis dolorem',
        comment:
          'ut voluptatem corrupti velit\nad voluptatem maiores\net nisi velit vero accusamus maiores\nvoluptates quia aliquid ullam eaque',
      },
      {
        id: 9,
        author: 'provident id voluptas',
        comment:
          'sapiente assumenda molestiae atque\nadipisci laborum distinctio aperiam et ab ut omnis\net occaecati aspernatur odit sit rem expedita\nquas enim ipsam minus',
      },
      {
        id: 10,
        author: 'eaque et deleniti atque tenetur ut quo ut',
        comment:
          'voluptate iusto quis nobis reprehenderit ipsum amet nulla\nquia quas dolores velit et non\naut quia necessitatibus\nnostrum quaerat nulla et accusamus nisi facilis',
      },

      {
        id: 11,
        author: 'eaque et deleniti atque tenetur ut quo ut',
        comment:
          'voluptate iusto quis nobis reprehenderit ipsum amet nulla\nquia quas dolores velit et non\naut quia necessitatibus\nnostrum quaerat nulla et accusamus nisi facilis',
      },

      {
        id: 12,
        author: 'eaque et deleniti atque tenetur ut quo ut',
        comment:
          'voluptate iusto quis nobis reprehenderit ipsum amet nulla\nquia quas dolores velit et non\naut quia necessitatibus\nnostrum quaerat nulla et accusamus nisi facilis',
      },

      {
        id: 13,
        author: 'eaque et deleniti atque tenetur ut quo ut',
        comment:
          'voluptate iusto quis nobis reprehenderit ipsum amet nulla\nquia quas dolores velit et non\naut quia necessitatibus\nnostrum quaerat nulla et accusamus nisi facilis',
      },

      {
        id: 14,
        author: 'eaque et deleniti atque tenetur ut quo ut',
        comment:
          'voluptate iusto quis nobis reprehenderit ipsum amet nulla\nquia quas dolores velit et non\naut quia necessitatibus\nnostrum quaerat nulla et accusamus nisi facilis',
      },

      {
        id: 15,
        author: 'eaque et deleniti atque tenetur ut quo ut',
        comment:
          'voluptate iusto quis nobis reprehenderit ipsum amet nulla\nquia quas dolores velit et non\naut quia necessitatibus\nnostrum quaerat nulla et accusamus nisi facilis',
      },
    ]);

    const addComment = (data) => {
      const newComment = {
        id: Math.random(),
        author: data.name || 'Анонім',
        comment: data.comment,
      };

      comments.value.unshift(newComment);
    };
    const openModal = () => {
      isModalOpen.value = true;
    };

    const closeModal = () => {
      isModalOpen.value = false;
    };

    const loadMore = () => {
      maxCommentsToShow.value += 5;
    };

    const slicedComments = computed(() => comments.value.slice(0, maxCommentsToShow.value));

    return {
      isModalOpen,
      openModal,
      rating,
      closeModal,
      slicedComments,
      addComment,
      loadMore,
      maxCommentsToShow,
      maxComments: comments.value.length,
    };
  },
};
</script>

<style>
*,
::before,
::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  height: 100%;
  font-family: Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  height: 100%;
  font-size: 18px;
  line-height: 1;
}

h1 {
  font-size: 32px;
}

img {
  border: 0;
  height: auto;
  max-width: 100%;
}

ul {
  list-style: none;
}

a {
  text-decoration: none;
}

.visually-hidden {
  clip-path: inset(50%);
  border: 0;
  clip: rect(1px, 1px, 1px, 1px);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  white-space: nowrap;
  width: 1px;
}

#app {
  height: 100%;
}

.container {
  max-width: 1230px;
  padding: 0 15px;
  margin: 0 auto;
}

.page-title {
  color: #fff;
  background-color: #07567e;
  text-align: center;
  padding: 20px 0;
  text-transform: uppercase;
}

.doctor-fullname {
  color: #14c1c5;
  text-transform: uppercase;
}

.doctor-info-main {
  display: flex;
  align-items: center;
  gap: 10px;
}

.star-rating {
  color: rgb(188, 175, 175);
}

.doctor-info-other {
  display: flex;
  gap: 20px;
  padding: 10px;
  border: 1px solid #ccc;
}

.doctor-photo {
  flex-shrink: 0;
  width: 219px;
  height: 243px;
}

.doctor-photo img {
  max-height: 100%;
  object-fit: cover;
  object-position: center top;
  width: 100%;
}

.info-block {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 100%;
}

.info-table {
  border-spacing: 30px 0;
}

.info-table td:first-child {
  white-space: nowrap;
  vertical-align: baseline;
}

.info-items {
  flex-shrink: 0;
}

.info-item {
  display: flex;
  column-gap: 20px;
}

.leave-comment-btn {
  align-self: flex-end;
}
</style>
