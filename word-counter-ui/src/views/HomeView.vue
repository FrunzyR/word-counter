<template>
    <div class="container">
        <div class="first-column">
            <h1>Youtube caption word counter</h1>
            <div class="flex flex-column gap-2">
                <label for="selectedOption">Select content type</label>
                <Dropdown id="selectedOption" v-model="selectedOption" :options="options" optionLabel="name" class="w-full" />
            </div>
            <div class="flex flex-column gap-2">
                <label for="url">Paste the link of a {{ selectedOption.name }}</label>
                <InputText id="url" v-model="videoURLInput" placeholder="Your URL"/>
            </div>
            <Button label="Analyse" :disabled="!videoURLInput" @click="$router.push('analysis')"/>
        </div>

        <div class="second-column">
            <VideoPreview />
        </div>
    </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import VideoPreview from '@/components/VideoPreview.vue'
import { useVideoStore } from '@/stores/video';
import router from '@/router';

const options = ref([
    { name: 'Playlist' },
    { name: 'Video' },
])
const selectedOption = ref(options.value[0]);

const videoStore = useVideoStore()

const videoURLInput = computed({
  get() {
    return videoStore.videoURL
  },
  set(val) {
    videoStore.changeVideoURL(val)
  }
})
</script>

<style scoped>
.container {
    height: inherit;

    display: flex;
    font-size: large;
}

.first-column {
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    font-weight: bold;
    padding: 2%;
}

h1 {
    font-size: 80px;
    margin: 0;
}

.second-column {
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
}
</style>
