<script>
export default {
    props: {
        currentPage: null,
        totalPages: null
    },
    methods: {
        nextPage() {
            if (currentPage < totalPages) {
                currentPage++;
                this.emit('current_page', this.currentPage)
            }
        },
        previousPage() {
            if (currentPage > 1) {
                currentPage--;
                this.emit('current_page', this.currentPage)
            }
        }
    }
}
</script>
<template>
    <!-- component -->
    <div class=" max-w-lg container flex justify-center mx-auto">
        <div class="flex flex-row mx-auto">
            <button type="button" @click="previousPage" :disabled="currentPage === 1"
                class="bg-gray-800 text-white rounded-l-md border-r border-gray-100 py-2 hover:bg-red-700 hover:text-white px-3">
                <div class="flex flex-row align-middle">
                    <svg class="w-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
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
                    <svg class="w-5 ml-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd"
                            d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z"
                            clip-rule="evenodd"></path>
                    </svg>
                </div>
            </button>
        </div>
    </div>
</template>