<template>
  <q-page
    class="row items-center justify-evenly"
    :style="`--background-image: url(${backgroundImageSrc})`"
  >
    <q-btn
      color="primary"
      label="Изменить фоновое изображение"
      @click="changeBackgroundImage"
    ></q-btn>
  </q-page>
</template>

<script lang="ts">
import { Picture } from 'components/models';
import { defineComponent, ref, Ref } from 'vue';

function useButtonClick(pictures: Ref<Picture[]>) {
  const backgroundImageIndex = ref(0);
  const backgroundImageSrc = ref(pictures.value[0].src);

  function changeBackgroundImage() {
    if (backgroundImageIndex.value < pictures.value.length - 1) {
      backgroundImageIndex.value += 1;
    } else {
      backgroundImageIndex.value = 0;
    }

    backgroundImageSrc.value = pictures.value[backgroundImageIndex.value].src;
  }

  return { backgroundImageSrc, changeBackgroundImage };
}

export default defineComponent({
  name: 'IndexPage',
  setup() {
    const pictures = ref<Picture[]>([
      {
        src: 'https://images.unsplash.com/photo-1548222606-6c4f581fd09d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1197&q=80',
      },
      {
        src: 'https://images.unsplash.com/photo-1589642314445-999ac13b0075?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1173&q=80',
      },
      {
        src: 'https://images.unsplash.com/photo-1596627008830-41d373a44a96?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1632&q=80',
      },
      {
        src: 'https://images.unsplash.com/photo-1547626740-02cb6aed9ef8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80',
      },
      {
        src: 'https://images.unsplash.com/photo-1548598187-35e00175d911?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1074&q=80',
      },
    ]);

    return { pictures, ...useButtonClick(pictures) };
  },
});
</script>

<style>
.q-page {
  background: var(--background-image) no-repeat center;
  background-size: cover;
}
</style>
