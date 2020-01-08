<template>
    <div class="container d-flex justify-content-center px-0">
        <div class="col-md-10 px-0">
            <div class="navbar subbar justify-content-between flex-nowrap flex-row py-3">

                <router-link to="/posts" class="dropdown-item" style="width: auto">
                    <span><i class="fas fa-user-edit"></i> {{ trans.nav.user.posts }}</span>
                </router-link>
                <router-link to="/tags" class="dropdown-item" style="width: auto">
                    <span><i class="fas fa-tags"></i> {{ trans.nav.user.tags }}</span>
                </router-link>
                <router-link to="/topics" class="dropdown-item" style="width: auto">
                    <span><i class="fas fa-lightbulb"></i> {{ trans.nav.user.topics }}</span>
                </router-link>
                <router-link to="/stats" class="dropdown-item" style="width: auto">
                    <span><i class="fas fa-chart-bar"></i> {{ trans.nav.user.stats }}</span>
                </router-link>

                <ul class="navbar-nav mr-auto flex-row float-right">
                    <li class="text-muted font-weight-bold">
                        <slot name="status"></slot>
                    </li>
                </ul>

                <div class="my-auto ml-auto">
                    <slot name="action"></slot>
                </div>

                <slot name="menu"></slot>
            </div>
        </div>
    </div>
</template>

<script>
    import md5 from 'md5'
    import axios from 'axios'

    export default {
        name: 'page-header',

        data() {
            return {
                user: Canvas.user,
                token: document.head.querySelector('meta[name="csrf-token"]')
                    .content,
                trans: JSON.parse(Canvas.lang),
            }
        },

        methods: {
            /**
             * Generate an MD5 hash from a given email to retrieve a Gravatar.
             *
             * @returns {string}
             */
            gravatar() {
                let hash = md5(this.user.email.toLowerCase().trim())

                return 'https://secure.gravatar.com/avatar/' + hash + '?s=200'
            }
        },
    }
</script>

<style scoped>
    a.dropdown-item:active {
        background-color: #f8f9fa;
        color: #16181b;
    }
</style>
