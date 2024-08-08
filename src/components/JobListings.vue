<script setup>
import { RouterLink } from 'vue-router';
import JobListing from "./JobListing.vue";
import { defineProps, onMounted, reactive } from "vue";
import PulseLoader from 'vue-spinner/src/PulseLoader.vue';
import axios from 'axios';

defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false
    }
});

const state = reactive({
    jobs: [],
    isLoading: true
});

onMounted(async () => {
    try {
        const response = await axios.get('http://localhost:8000/jobs');
        state.jobs = response.data;
    } catch (error) {
        console.error('Error Fetching Jobs', error);
    } finally {
        state.isLoading = false;
    }
});
</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-[#660e60] mb-6 text-center">
                Browse Jobs
            </h2>

            <!-- show loading spinner while loading is true-->
            <div v-if="state.isLoading" class="text-center text-[#f012e1] py-6">
                <PulseLoader/>
            </div>
            <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>

    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
        <RouterLink to="/jobs"
            class="block bg-[#660e60] text-white text-center py-4 px-6 rounded-xl hover:bg-[#893f71]">
            View All Jobs
        </RouterLink>
    </section>
</template>
