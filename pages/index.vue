<template>
  <div>
    <app-container>
      <transition name="fade">
        <app-popup v-if="isPopupShown">
          <app-editing-item-form />
        </app-popup>
      </transition>
      <app-shopping-list />
    </app-container>
  </div>
</template>

<script>
import Container from '@/components/shared/Container';
import ShoppingList from '@/components/blocks/ShoppingList';
import Popup from '@/components/service/Popup';
import EditingItemForm from '@/components/blocks/EditingItemForm';
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
    'app-shopping-list': ShoppingList,
    'app-popup': Popup,
    'app-editing-item-form': EditingItemForm,
  },
  computed: {
    isPopupShown() {
      return this.$store.getters['popup/getPopupVisibility'];
    },
  },
};
</script>

<style scoped></style>
