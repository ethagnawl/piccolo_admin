<template>
    <div class="sidebar">
        <p class="opaque">
            <router-link class="subtle" to="/">
                <font-awesome-icon icon="home" />Home
            </router-link>
        </p>
        <p class="opaque" v-on:click="isHiddenTables = !isHiddenTables">
            <font-awesome-icon icon="table" />Tables
            <span style="float: right">
                <font-awesome-icon
                    icon="angle-down"
                    title="Show tables"
                    v-if="isHiddenTables"
                />
                <font-awesome-icon icon="angle-up" title="Hide tables" v-else />
            </span>
        </p>
        <TableNav v-show="!isHiddenTables" />
        <p
            class="opaque"
            v-if="formConfigs.length > 0"
            v-on:click="isHiddenForms = !isHiddenForms"
        >
            <font-awesome-icon icon="cogs" />Forms
            <span style="float: right">
                <font-awesome-icon
                    icon="angle-down"
                    title="Show forms"
                    v-if="isHiddenForms"
                />
                <font-awesome-icon icon="angle-up" title="Hide forms" v-else />
            </span>
        </p>
        <FormNav v-show="!isHiddenForms" />
    </div>
</template>

<script>
import Vue from "vue"
import TableNav from "./TableNav.vue"
import FormNav from "./FormNav.vue"

export default Vue.extend({
    data() {
        return {
            isHiddenTables: false,
            isHiddenForms: false,
        }
    },
    components: {
        TableNav,
        FormNav,
    },
    computed: {
        formConfigs() {
            return this.$store.state.formConfigs
        },
    },
})
</script>

<style lang="less">
@import "../vars.less";

div.sidebar {
    background-color: rgba(0, 0, 0, 0.1);
    height: 100%;

    p {
        padding: 0.5rem;
        margin: 0;
        cursor: pointer;
        user-select: none;

        a {
            display: block;
            text-decoration: none;
        }
    }

    ul {
        margin: 0;
        padding: 0;

        li {
            list-style: none;
            text-transform: capitalize;

            a {
                align-items: center;
                display: flex;
                padding: 0.5rem;
                text-decoration: none;
                border-left: 3px solid rgba(0, 0, 0, 0);

                &:hover {
                    background-color: rgba(0, 0, 0, 0.2);
                }

                &.active {
                    border-left: 3px solid @light_blue;
                }

                svg {
                    transform: rotate(90deg);
                }

                span {
                    display: block;
                    box-sizing: border-box;
                    padding: 0 0.5rem;
                    user-select: none;
                }
            }
        }
    }
}
</style>
