<script>
import json from "@/../src/json/wallpapers.json"
import Pagination from '@/components/Pagination.vue';

export default {
    name: 'Main',
    components: {
        Pagination
    },
    data() {
        return {
            title: 'Laracast Wallpapers',
            content: 'Don’t forget! Every series has it’s own dedicated wallpaper. Whenever you view a series, scroll right under the video and you’ll see a download button there.Go ahead and explore and find your favorite one. Here are a few with Lary!',
            wallpapers: json.wallpapers,
            pageSize: 5, // Number of items per page
            currentPage: 1 // Current page
        }
    },
    computed: {
        totalPages() {
            return Math.ceil(this.wallpapers.length / this.pageSize);
        },
        paginatedItems(current_page) {
            const startIndex = (this.currentPage - 1) * this.pageSize;
            const endIndex = startIndex + this.pageSize;
            return this.wallpapers.slice(startIndex, endIndex);
        }
    },
}
</script>

<template>
    <div class="section pb-8 lg:pb-10">
        <div class="container">
            <main class="flex items-center justify-center">
                <div class="max-w-3xl flex-1">
                    <div>
                        <header class="mb-8">
                            <h1 class="text-2xl font-medium">{{ title }}</h1>
                            <p class="text-grey-600 text-sm mt-2">{{ content }}</p>
                        </header>
                        <div v-for="wallpaper in paginatedItems" :key="wallpaper.id" class="mb-12">
                            <a :href="wallpaper.img">
                                <img :src="wallpaper.img" :alt="wallpaper.alt" class="mb-4 w-full rounded-md" />
                            </a>
                            <div class="flex justify-center items-center">
                                <a :href="wallpaper.img" class="button" download="">Download Wallpaper</a>
                            </div>
                        </div>
                        <Pagination @current_page="paginatedItems" :currentPage="currentPage" :totalPages="totalPages">
                        </Pagination>
                    </div>
                </div>
            </main>
        </div>
    </div>
</template>