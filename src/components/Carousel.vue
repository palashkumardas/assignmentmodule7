<script setup>
import { ref, reactive, onMounted, onBeforeUnmount, nextTick } from 'vue'

const items = ref([
    {
        title:'Slide Image One',
        url:'https://media.istockphoto.com/id/1201252148/photo/butterflies.webp?b=1&s=170667a&w=0&k=20&c=qJBeZMc_VGAubUWPmfygDgm0wXnrSs2IeK5n53fTXjQ='
    },
    {
        title:'Slide Image Two',
        url:'https://images.unsplash.com/photo-1470240731273-7821a6eeb6bd?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OXx8c3ByaW5nfGVufDB8fDB8fHww&auto=format&fit=crop&w=500&q=60'
    },
    {
        title:'Slide Image Three',
        url:'https://images.unsplash.com/photo-1472214103451-9374bd1c798e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8bmF0dXJlfGVufDB8fDB8fHww&auto=format&fit=crop&w=500&q=60'
    },
    {
        title:'Slide Image Four',
        url:'https://images.unsplash.com/photo-1500382017468-9049fed747ef?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MzJ8fG5hdHVyZXxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60'
    },
])

let carousel = null

onMounted(() =>{
    carousel = new Flickity( '#carousel', {
        autoPlay:2000
    });
})

onBeforeUnmount(() => {
    carousel.destroy()
})

let newItem = reactive({
    title:'',
    url:''
})

function updateCarousel(){
    items.value.push(newItem)
    console.log(items)
    carousel.destroy()

    nextTick(() =>{
        carousel = new Flickity( '#carousel', {});
    })
}

</script>
<template>
    <form>
        <div class="grid gap-6 mb-6 md:grid-cols-3">
        <div>
            <input v-model="newItem.url" type="text" id="color-name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-yellow-500 focus:border-yellow-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Image URL">
        </div>
        <div>
            <input v-model="newItem.title" type="text" id="color-name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-yellow-500 focus:border-yellow-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Title">
        </div>

        <div>
            <button @click.prevent="updateCarousel()" type="submit" class="text-white bg-yellow-700 hover:bg-yellow-800 focus:ring-4 focus:outline-none focus:ring-yellow-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-yellow-600 dark:hover:bg-yellow-700 dark:focus:ring-yellow-800">Add New Item</button>
        </div>        
        </div>
    </form>
    <div class="mx-auto items" id="carousel">
        <div class="item" :style="`background-image:url(${item.url})`" v-for="(item, index) in items" :key="index">
            <p class="pl-12 pr-12 pt-80 text-white font-bold ">{{ item.title }}</p>
        </div>
    </div>    
</template>

<style scoped>
.items{
    width: 1000px;
    height:400px;
}

.item{
    width: 1000px;
    height: 400px;
    background-color: gray;
    background-size: cover;
}
</style>
