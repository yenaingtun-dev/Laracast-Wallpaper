<script>
export default {
    name: 'Header',
    data() {
        return {
            link: 'https://laracasts.com',
            logo: '/logo-white.svg',
            alt: 'Laracasts'
        }
    }
}
</script>

<template>
    <header class="section py-6 px-5 mb-8 flex items-center justify-center">
        <h1 class="inline-block">
            <a :href="link">
                <img :alt="alt" :src="logo" width="170">
            </a>
        </h1>
    </header>
</template>