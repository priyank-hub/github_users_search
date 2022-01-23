<template>
    <div>
        <div class="">
            <span class="" style="font-size: 3vh; font-weight: 900; letter-spacing: 1px">
                <i class="fab fa-git-alt"></i>
                <span class="">
                    Repositories
                </span>
            </span>
        </div>
        <div class="inner-card my-3">
            <v-card
                elevation="4"
                class="section my-4 p-3"
                v-for="(repo, index) in repos" :key="index"
            >
                {{ repo.name }}
            </v-card>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Repos',
    components: {

    },
    props: {
        repos: Array,
        user: Object,
    },
    mounted() {

    },
    methods: {

    }

}
</script>
