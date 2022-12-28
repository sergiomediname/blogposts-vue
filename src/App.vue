<script setup>
import { computed, ref } from "vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";
import HeaderBlog from "./components/HeaderBlog.vue";
import PaginationPosts from "./components/PaginationPosts.vue";
import BlogPost from "./components/BlogPost.vue";

const posts = ref([]);
const favorite = ref("");
const postPerPage = 10;
const start = ref(0);
const end = ref(postPerPage);
const maxPosts = computed(() => posts.value.length);
const loading = ref(true);

const addFavorite = (title) => (favorite.value = title);
const nextPage = () => {
    start.value = start.value + postPerPage;
    end.value = end.value + postPerPage;
};
const prevPage = () => {
    start.value = start.value - postPerPage;
    end.value = end.value - postPerPage;
};

fetch("https://jsonplaceholder.typicode.com/posts/")
    .then((res) => res.json())
    .then((data) => (posts.value = data))
    .catch((e) => console.log(e))
    .finally(() => (loading.value = false));
</script>

<template>
    <div class="container">
        <HeaderBlog />
        <main>
            <div class="vb-favorite alert alert-warning" role="alert">
                Mi post favorito: {{ favorite }}
            </div>
            <LoadingSpinner v-if="loading" />
            <div class="vb-blog" v-else>
                <PaginationPosts
                    @nextPage="nextPage"
                    @prevPage="prevPage"
                    :start="start"
                    :end="end"
                    :maxPosts="maxPosts"
                />
                <div class="vb-items row">
                    <BlogPost
                        v-for="post in posts.slice(start, end)"
                        :title="post.title"
                        :body="post.body"
                        :id="post.id"
                        :key="post.id"
                        @addFavorite="addFavorite(post.title)"
                    />
                </div>
            </div>
        </main>
        <footer>
            <button class="btn btn-secondary">view on github</button>
        </footer>
    </div>
</template>
