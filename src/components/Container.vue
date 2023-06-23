<template>
  <div>
    <div v-for="data in PostData" :key="i">
        <Post :data="data"/>
    </div>
  </div>
</template>

<script>
import Post from './Post.vue';
export default {
  name: 'Container',
  components: {
    Post : Post
  },
  props: {
    PostData : Array
  }
}
</script>

<style>

</style>