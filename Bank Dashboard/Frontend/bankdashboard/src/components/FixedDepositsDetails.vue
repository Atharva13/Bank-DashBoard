<template>
    <div v-if="!!visibility()">
        <p class="mt-2">{{type}}</p>
        <p class="mt-n3">ROI - {{roi}} %</p>
        <p class="mt-n3">
            Min Max Amount: {{ amount }} GBP
        </p>
        <p class="mt-n3">
            Term: {{ term }} years
        </p>
    </div>
</template>

<script>
export default {
    props: ['type','roi','transaction','amount','term'],
    methods: {
        visibility() {
            if(this.term === undefined)
            {
                return false;
            }
            return true;
        }
    }
}
</script>