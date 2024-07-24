<script setup>
import JobListing from './JobListing.vue';
import jobData from "@/jobs copy.json";
import { ref } from "vue";

const jobs = ref(jobData);

</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-[#660e60] mb-6 text-center">
                Browse Jobs
            </h2>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <JobListing v-for="job in jobs" :key="job.id" :job="job" />

        </div>
    </section>
</template>
