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
                class="section my-5 p-2"
                v-for="(repo, index) in repos" :key="index"
            >   
                <div class="d-flex flex-row justify-content-between">
                    <div class="col-10">
                        {{ repo.name }}
                    </div>

                    <div class="col-2 text-right">
                        <a :href="repo.html_url" target="_blank">
                            <i class="fas fa-external-link-alt"></i>
                        </a>
                    </div>
                </div>
                <div class="d-flex flex-row">
                    <div class="col-12 py-0">
                        <span class="text-muted" style="font-size: 13px">
                            {{ repo.description }}
                        </span>
                    </div>
                </div>
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
