<script>
import json from "@/../src/json/wallpapers.json"

export default {
    name: 'Main',
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
        paginatedItems() {
            const startIndex = (this.currentPage - 1) * this.pageSize;
            const endIndex = startIndex + this.pageSize;
            return this.wallpapers.slice(startIndex, endIndex);
        }
    },
    methods: {
        nextPage() {
            if (this.currentPage < this.totalPages) {
                this.currentPage++;
            }
        },
        previousPage() {
            if (this.currentPage > 1) {
                this.currentPage--;
            }
        }
    }
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
                        <!-- component -->
                        <div class=" max-w-lg container flex justify-center mx-auto">
                            <div class="flex flex-row mx-auto">
                                <button type="button" @click="previousPage" :disabled="currentPage === 1"
                                    class="bg-gray-800 text-white rounded-l-md border-r border-gray-100 py-2 hover:bg-red-700 hover:text-white px-3">
                                    <div class="flex flex-row align-middle">
                                        <svg class="w-5 mr-2" fill="currentColor" viewBox="0 0 20 20"
                                            xmlns="http://www.w3.org/2000/svg">
                                            <path fill-rule="evenodd"
                                                d="M7.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l2.293 2.293a1 1 0 010 1.414z"
                                                clip-rule="evenodd"></path>
                                        </svg>
                                        <p class="ml-2">Prev</p>
                                    </div>
                                </button>
                                <span class="bg-gray-800 text-white rounded-r-md py-2  border-gray-200 px-5">{{
                                currentPage }}</span>
                                <button type="button" @click="nextPage" :disabled="currentPage === totalPages"
                                    class="bg-gray-800 text-white rounded-r-md py-2 border-l border-gray-200 hover:bg-red-700 hover:text-white px-3">
                                    <div class="flex flex-row align-middle">
                                        <span class="mr-2">Next</span>
                                        <svg class="w-5 ml-2" fill="currentColor" viewBox="0 0 20 20"
                                            xmlns="http://www.w3.org/2000/svg">
                                            <path fill-rule="evenodd"
                                                d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z"
                                                clip-rule="evenodd"></path>
                                        </svg>
                                    </div>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </main>
        </div>
    </div>
</template>