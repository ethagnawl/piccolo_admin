<template>
    <div
        :class="{error: apiResponseMessage.type == 'error'}"
        id="message_popup"
        v-if="visible"
    >
        <p class="message">{{ message }}</p>
        <p class="close">
            <a
                class="subtle"
                href="#"
                v-on:click.prevent="visible = false"
            >
                <font-awesome-icon icon="times" />
            </a>
        </p>
    </div>
</template>


<script lang="ts">
import Vue from "vue"
import * as i from "../interfaces"

export default Vue.extend({
    data() {
        return {
            visible: false,
            timeLastAppeared: 0,
        }
    },
    computed: {
        message(): string {
            return this.apiResponseMessage
                ? this.apiResponseMessage.contents
                : "-"
        },
        apiResponseMessage(): i.APIResponseMessage {
            return this.$store.state.apiResponseMessage
        },
    },
    methods: {
        getTime(): number {
            return new Date().getTime()
        },
    },
    watch: {
        visible() {
            this.timeLastAppeared = this.getTime()
        },
        apiResponseMessage() {
            this.visible = true
            const app = this

            setTimeout(() => {
                const now = this.getTime()
                // Only hide if it if it wasn't subsequently opened again.
                if (now - app.timeLastAppeared >= 3000) {
                    app.visible = false
                }
            }, 3000)
        },
    },
})
</script>


<style lang="less">
@import "../vars.less";

div#message_popup {
    display: flex;
    position: fixed;
    bottom: 0;
    width: 100%;
    padding: 0.5rem 1rem;
    box-sizing: border-box;
    background-color: green;

    p,
    a {
        color: white !important;
    }

    p.message {
        flex-grow: 1;
        text-align: center;
    }

    p.close {
        flex-grow: 0;
    }
}
div#message_popup.error {
    background-color: @red;
}
</style>
