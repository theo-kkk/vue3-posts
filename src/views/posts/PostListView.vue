<template>
  <div>
    <h2>게시글 리스트</h2>
    <hr class="my-4" />
    <div class="row g-3">
      <div v-for="post in posts" :key="post.id" class="col-4">
        <PostItem
          :title="post.title"
          :content="post.content"
          :created-at="post.createdAt"
          @click="goPage(post.id)"
        ></PostItem>
      </div>
    </div>
  </div>
</template>

<script setup>
import PostItem from '@/components/posts/PostItem.vue'
import { useRouter } from 'vue-router'
import { getPosts } from '@/api/posts'
import { ref } from 'vue'

const router = useRouter()

const posts = ref([])

const fetchPosts = () => {
  posts.value = getPosts()
}
fetchPosts()

const goPage = (postId) => {
  // router.push(`/posts/${postId}`)
  router.push({ name: 'PostDetail', params: { id: postId } })
}
</script>

<style lang="scss" scoped></style>
