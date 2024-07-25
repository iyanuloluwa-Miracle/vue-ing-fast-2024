<script setup>
import { defineProps, ref, computed } from 'vue';

const props = defineProps({
    job:Object,

})


const showFullDescription = ref(false);


const toggleFullDescription = () =>{
    showFullDescription.value = !showFullDescription.value;
}


const truncatedDescription = computed(()=>{
    let description = props.job.description;
    if(!showFullDescription.value){
        description = description.substring(0, 90) + '...'

    }
    return description;
})

</script>




<template>
    <div class="bg-white rounded-xl shadow-md relative">
        <div class="p-4">
            <div class="mb-6">
                <div class="text-[#00202e] my-2 font-extrabold">{{ job.type }}</div>
                <h3 class="text-xl font-extrabold">{{ job.title }}</h3>
            </div>

            <div class="mb-5">
                <div>
                    {{ truncatedDescription }}

                </div>

                <button @click="toggleFullDescription" class="text-[#660e60] hover:text-[#893f71] mb-5">
                    {{ showFullDescription ? 'Less' : 'More' }}

                </button>

            </div>

            <h3 class="text-[#660e60] mb-2 font-extrabold">{{  job.salary }}</h3>

            <div class="border border-gray-100 mb-5"></div>

            <div class="flex flex-col lg:flex-row justify-between mb-4 font-extrabold">
                <div class="text-orange-700 mb-3">
                    <i class="pi pi-map-marker text-[#660e60] "></i>
                    {{ job.location }}
                </div>
                <a :href="'/job/' + job.id"
                    class="h-[36px] bg-[#660e60] hover:bg-[#893f71] text-white px-4 py-2 rounded-lg text-center text-sm">
                    Read More
                </a>
            </div>
        </div>
    </div>

</template>



