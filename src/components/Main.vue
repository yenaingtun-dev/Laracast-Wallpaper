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
            pageSize: 5,
            currentPage: 1,
            search: '',
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
        },
        filteredList() {
            return this.wallpapers.filter(wallpaper => {
                return wallpaper.alt.toLowerCase().includes(this.search.toLowerCase())
            })
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
                        <div class="relative text-gray-700 mb-10 w-3/4">
                            <label for="Search" class="sr-only"> Search Laracast Course Title </label>

                            <input v-model="search" type="text" id="Search" placeholder="Search Laracast Course Title"
                                class="w-full rounded-md border-gray-200 py-2.5 pe-10 shadow-sm sm:text-sm" />

                            <span class="absolute inset-y-0 end-0 grid w-10 place-content-center">
                                <button type="button" class="text-gray-600 hover:text-gray-700">
                                    <span class="sr-only">Search</span>

                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                        stroke-width="1.5" stroke="currentColor" class="h-4 w-4">
                                        <path stroke-linecap="round" stroke-linejoin="round"
                                            d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
                                    </svg>
                                </button>
                            </span>
                        </div>
                        <div v-if="search.length > 0">
                            <div v-for="wallpaper in filteredList" :key="wallpaper.id" class="mb-12">
                                <a :href="wallpaper.img">
                                    <img :src="wallpaper.view" :alt="wallpaper.alt"
                                        class="mb-4 w-full h-full rounded-md" :key="wallpaper.id" loading="lazy" />
                                </a>
                                <div class="flex justify-center items-center">
                                    <a :href="wallpaper.img" class="button" download="">Download Wallpaper</a>
                                </div>
                            </div>
                        </div>
                        <div v-else v-for="wallpaper in paginatedItems" :key="wallpaper.id" class="mb-12">
                            <a :href="wallpaper.img">
                                <!-- <div>
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                        stroke-width="1.5" stroke="currentColor" class="animate-spin w-6 h-6 mx-auto">
                                        <path stroke-linecap="round" stroke-linejoin="round"
                                            d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0 3.181 3.183a8.25 8.25 0 0 0 13.803-3.7M4.031 9.865a8.25 8.25 0 0 1 13.803-3.7l3.181 3.182m0-4.991v4.99" />
                                    </svg>
                                </div> -->
                                <img :src="wallpaper.view" :alt="wallpaper.alt" class="mb-4 w-full h-full rounded-md"
                                    :key="wallpaper.id" loading="lazy" />
                            </a>
                            <div class="flex justify-center items-center">
                                <a :href="wallpaper.img" class="button" download="">Download Wallpaper</a>
                            </div>
                        </div>
                        <div class="max-w-lg container flex justify-center mx-auto" v-if="!search.length > 0">
                            <div class="flex flex-row mx-auto">
                                <button type="button" @click="previousPage" :disabled="currentPage === 1"
                                    class="bg-gray-800 text-white rounded-l-md border-r border-gray-100 py-2 hover:bg-white hover:text-[#151f32] px-3">
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
                                    class="bg-gray-800 text-white rounded-r-md py-2 border-l border-gray-200 hover:bg-white hover:text-[#151f32] px-3">
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