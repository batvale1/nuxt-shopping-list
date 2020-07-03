<template>
  <div class="single-item">
    <app-container>
      <h1 class="single-item__heading">Purchase № {{ currentItem.id }}</h1>
      <p class="single-item__text">Name: {{ currentItem.name }}</p>
      <p class="single-item__text">Price: {{ currentItem.price }} $</p>
      <p class="single-item__text">Date: {{ currentItem.date }}</p>
      <p class="single-item__text">Additional info and actions...</p>
    </app-container>
  </div>
</template>

<script>
import Container from '@/components/shared/Container';
export default {
  data() {
    return {
      metas: {
        meta_title: 'Shopping list',
        meta_description: 'тестовое задание',
        meta_keywords: 'тестовое задание',
      },
    };
  },
  head() {
    if (this.metas) {
      return {
        title: this.metas.meta_title,
        meta: [
          {
            hid: 'description',
            name: 'description',
            content: this.metas.meta_description || '',
          },
          {
            hid: 'keywords',
            name: 'keywords',
            content: this.metas.meta_keywords || '',
          },
          {
            hid: 'og:title',
            property: 'og:title',
            content: this.metas.meta_title || '',
          },
          {
            hid: 'og:description',
            property: 'og:description',
            content: this.metas.meta_description || '',
          },
        ],
      };
    }
  },
  components: {
    'app-container': Container,
  },
  computed: {
    currentItem() {
      return this.$store.getters['shopping-list/getCurrentSingleItem'];
    },
  },
  async fetch({ store, route, error }) {
    await store
      .dispatch('shopping-list/getSingleItem', { id: route.params.id })
      .catch((e) => {
        error({ statusCode: 404, message: 'Item not found' });
      });
  },
};
</script>

<style scoped>
.single-item {
  color: #fff;
  margin: 30px;
}

.single-item__heading {
  margin-bottom: 30px;
}

.single-item__text {
  font-size: 20px;
  margin-bottom: 10px;
}

.single-item__text:last-of-type {
  margin-bottom: 0;
}
</style>
