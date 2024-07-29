<script setup lang="ts">
import { toRef} from 'vue'
import { type Event } from '@/types'

const props = defineProps<{
    event: Event
    id: String
}>()
// eslint-lisable-next-line @typescript-eslint/no-unused-vars
const { event } = toRef(props)
</script>

<template>
    <p>Edit event here</p>
</template>
