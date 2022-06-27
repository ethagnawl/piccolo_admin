<template>
    <BaseView>
        <div class="api-response-message">
            <h1>{{ apiResponseMessage.formName }}</h1>
            <h2>Results:</h2>
            <p>{{ apiResponseMessage.contents }}</p>
        </div>
    </BaseView>
</template>

<script lang="ts">
import Vue from "vue"
import BaseView from "./BaseView.vue"

export default Vue.extend({
    components: {
        BaseView,
    },
    computed: {
        apiResponseMessage() {
            return this.$store.state.apiResponseMessage
        },
    },
    mounted() {
        this.$store.commit("updateCurrentTablename", "")
    },
})
</script>

<style scoped lang="less">
div.api-response-message {
    padding: 0 1rem;
}
</style>
