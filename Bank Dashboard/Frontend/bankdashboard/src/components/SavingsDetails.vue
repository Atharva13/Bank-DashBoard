<template>
    <div v-if="!!visibility()">
        <p class="mt-2">{{type}}</p>
        <p class="mt-n3">ROI - {{roi}} %</p>
        <p class="mt-n3">
        Max Transaction/ day {{transaction}} GBP
        </p>
    </div>
</template>

<script>
export default {
    props: ['type','roi','transaction'],
    methods: {
        visibility() {
            if(this.transaction === undefined)
            {
                return false;
            }
            return true;
        }
    }
}
</script>