<script setup>
    import { computed, onMounted, ref } from 'vue'
    import { useFhemStore } from '@/stores/fhem'

    const props = defineProps({
        el: Object,
        iconmap: Array,
        devices: Array,
        height: String
    })

    const fhem = useFhemStore()

    const height = ref(/=maximized$/.test(fhem.app.currentView) ? (window.innerHeight - 170) : props.height)

    const content = computed(() => {
        let src = fhem.handleDefs(props.el.html, ['text'],['', true]),
            res = {
                text: src.text
            }

        return res
    })
</script>

<template>
    <html 
        :height="height"
        style="border:none; width:100%;">
        {{ content.text }}     
    </html>
</template>