<template>
  <div>
    <div class="container">      
      <div class="row justify-content-between my-3">
        <div class="col-6 text-left py-0">
          <span style="font-weight: 900; font-size: 20px">
            GitFinder
          </span>
        </div>
        <div class="col-6 text-right py-0">
          <span>
            <b-button class="border-0" variant="light" style="" @click="darkMode">
              <div v-if="this.$vuetify.theme.dark">
                <span style="font-size: 13px; font-weight: 500; letter-spacing: 1px">
                  LIGHT
                </span>
                <i class="fas fa-sun mx-2"></i>
              </div>
              <div v-else>
                <span style="font-size: 13px; font-weight: 500; letter-spacing: 1px">
                  DARK
                </span>
                <i class="fas fa-moon mx-2"></i>
              </div>
            </b-button>
          </span>
        </div>
      </div>

      <div class="row my-2">
        <div class="col-12">
          <v-card
            elevation="4"
            class="section px-4"
          >
            <b-input-group class="align-items-center">
              <!-- <b-input-group-prepend>
                <b-button variant="" class="border-0" style="background-color: transparent">
                  <i class="fas fa-search text-primary"></i> 
                </b-button>
              </b-input-group-prepend> -->
              
              <v-text-field
                v-model="search"
                :error="error"
                class="mx-lg-4 mx-md-2"
                style=""
                placeholder="Search github username..."
                required
              ></v-text-field>

              <b-input-group-append class="">
                <b-button class="border-0 py-2 px-4 section" variant="primary" @click="searchUser">
                  <span style="font-size: 15px">
                    Search
                  </span>
                </b-button>
              </b-input-group-append>
            </b-input-group>
          </v-card>
        </div>
      </div>

      <div class="row my-3">
        <div class="col-12">
          <v-card
            elevation="4"
            class="section p-4 p-md-5"
          >
            <div class="row">           
              <div class="col-12 col-md-3 col-lg-2">
                <b-img :src="user.picture" class="" style="width: 100%" rounded="circle" alt="Circle image"></b-img>
              </div>
              
              <div class="col-12 col-md-9 col-lg-10 text-md-left text-lg-left">              
                <div class="row justify-content-between align-items-center">
                  <div class="col-12 col-md-6 col-lg-6 pb-0">
                    <span style="font-size: 24px; font-weight: 900; letter-spacing: 1px" v-if="user.name">
                      {{ user.name }}
                    </span>
                    <span v-else class="text-muted" style="font-size: 24px; font-weight: 900; letter-spacing: 1px">
                      Name Not Available
                    </span>
                  </div>
                  <div class="col-12 col-md-6 col-lg-6 py-0 text-lg-right">
                    <span style="font-size: 14px; font-weight: 700; letter-spacing: 1px">
                      Joined 
                      <span v-if="user.joined_date">
                        {{ joined(user.joined_date) }}
                      </span>
                      <span v-else class="text-muted">
                        Not Available
                      </span>
                    </span>
                  </div>
                </div>

                <div class="row">
                  <div class="col-12 py-0">
                    <span style="font-size: 15px" class="text-primary">
                      @{{ user.username }}
                    </span>
                  </div>
                </div>  
              
                <div class="row my-3 d-none d-md-none d-lg-block">
                  <div class="col-12 col-md-10">
                    <span class="text-muted" v-if="!user.bio">
                      This profile has no bio.
                    </span>
                    <span v-else>
                      {{ user.bio }}
                    </span>
                  </div>
                </div>
              </div>
            </div>

            <div class="row my-3 d-block d-md-block d-lg-none">
              <div class="col-12 col-md-10">
                <span class="text-muted" v-if="!user.bio">
                  This profile has no bio.
                </span>
                <span v-else class="text-muted">
                  {{ user.bio }}
                </span>
              </div>
            </div>

            <div class="row my-2">
              <div class="col-4 col-md-3 col-lg-2 d-none d-md-none d-lg-block py-0"></div>
              <div class="col-12 col-md-12 col-lg-10 py-0 inner-card">
                
                <v-card
                  elevation="4"
                  class="section"
                >
                  <div class="container my-2">
                    <div class="row">
                      <div class="col-12 col-md-4 text-center text-md-center text-lg-left">
                        <a href="#repos" :class="this.$vuetify.theme.dark ? 'text-white' : 'text-dark'">
                          <span style="font-size: 13px">
                            Repos
                          </span>
                          <div>
                            <span style="font-size: 20px; font-weight: 900">
                              {{ user.repos }}
                            </span>
                          </div>
                        </a>
                      </div>

                      <div class="col-12 col-md-4 text-center text-md-center text-lg-center">
                        <div>
                          <span style="font-size: 13px">
                            Followers
                          </span>
                        </div>
                        <div>
                          <span style="font-size: 20px; font-weight: 900">
                            {{ user.followers }}
                          </span>
                        </div>
                      </div>

                      <div class="col-12 col-md-4 text-center text-md-center text-lg-right">
                        <div>
                          <span style="font-size: 13px">
                            Following
                          </span>
                        </div>
                        <div>
                          <span style="font-size: 20px; font-weight: 900">
                            {{ user.following }}
                          </span>
                        </div>
                      </div>
                    </div>
                  </div>
                </v-card>

              </div>
            </div>

            <!-- icons -->
            <div class="row my-0">
              <div class="col-4 col-md-3 col-lg-2 d-none d-md-none d-lg-block"></div>
              <div class="col-12 col-md-12 col-lg-10">
                <div class="row">
                  <div class="col-12 col-md-6 col-lg-6 my-0 pb-0">
                    <span v-if="user.location">
                      <span>
                        <i class="fas fa-map-marker-alt"></i>
                      </span>
                      <span class="mx-3">
                        {{ user.location }}
                      </span>
                    </span>
                    <span v-else class="text-muted">
                      <span>
                        <i class="fas fa-map-marker-alt"></i>
                      </span>
                      <span class="mx-3">
                        Not Available
                      </span>
                    </span>
                  </div>

                  <div class="col-12 col-md-6 col-lg-6 my-0 pb-0">
                    <span class="" v-if="user.twitter">
                      <span>
                        <i class="fab fa-twitter"></i>
                      </span>
                      <span class="mx-3">
                        {{ user.twitter }}
                      </span>
                    </span>
                    <span v-else class="text-muted">
                      <span>
                        <i class="fab fa-twitter"></i>
                      </span>
                      <span class="mx-3">
                        Not Available
                      </span>
                    </span>
                  </div>

                  <div class="col-12 col-md-6 col-lg-6 my-0 pb-0">
                    <span class="" v-if="user.link">
                      <span>
                        <i class="fas fa-link"></i>
                      </span>
                      <span class="mx-3">
                        <a :href="user.link" target="_blank">
                          @{{ user.username }}
                        </a>
                      </span>
                    </span>
                    <span v-else class="text-muted">
                      <span>
                        <i class="fas fa-link"></i>
                      </span>
                      <span class="mx-3">
                        Not Available
                      </span>
                    </span>
                  </div>

                  <div class="col-12 col-md-6 col-lg-6 my-0">
                    <span class="" v-if="user.email">
                      <span>
                        <i class="fas fa-envelope"></i>
                      </span>
                      <span class="mx-3">
                        {{ user.email }}
                      </span>
                    </span>
                    <span v-else class="text-muted">
                      <span>
                        <i class="fas fa-envelope"></i>
                      </span>
                      <span class="mx-3">
                        Not Available
                      </span>
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </v-card>
        </div>
      </div>

      <div class="row my-5" v-if="repos.length > 0">
        <div class="col-12">
          <v-card elevation="4" class="section p-4 p-md-5">
            <section id="repos">
              <Repos :repos="repos" :user="user"/>
            </section>
          </v-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
import moment from 'moment'
import Repos from './Repos'

export default {
  name: 'Card',
  props: {
  
  },
  components: {
    Repos,
  },
  data() {
    return {
      search: '',
      user: {
        name: 'The Octocat',
        email: null,
        joined_date: null,
        username: 'Octocat',
        bio: null,
        repos: 0,
        repos_url: null,
        followers: 0,
        followers_url: '#',
        following: 0,
        following_url: '#',
        location: null,
        twitter: null,
        link: null,
        institution: null,
        picture: '/assets/user.png',
      },

      repos: [],
      error: false,
    }
  },
  methods: {
    
    darkMode() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
    async searchUser() {
      this.error = false;
      this.repos = [];
      try {
        let res =  await axios.get(`https://api.github.com/users/${this.search}`)
        // console.log('res', res);
        this.user.name = res.data.name;
        this.user.email = res.data.email;
        this.user.joined_date = res.data.created_at;
        this.user.username = res.data.login;
        this.user.bio = res.data.bio;
        this.user.repos = res.data.public_repos;
        this.user.repos_url = res.data.repos_url;
        this.user.followers = res.data.followers;
        this.user.following_url = res.data.following_url;
        this.user.following = res.data.following;
        this.user.followers_url = res.data.followers_url;
        this.user.location = res.data.location;
        this.user.twitter = res.data.twitter_username;
        this.user.link = res.data.html_url;
        this.user.institution = res.data.organizations_url;
        this.user.picture = res.data.avatar_url;
      } catch (error) {
        console.log('error', error);
        this.error = true;
      }

      try {
        const repo = await axios.get('https://api.github.com/users/' + this.user.username + '/repos');
        // console.log('repo', repo.data);
        this.repos = repo.data;  
      } catch (error) {
        console.log('error', error);
        this.error = true;
      }
    },
    joined(date) {
      console.log();
      let t = moment(date);
      return t.utc().format('DD MMMM YYYY');
    }
  }
}
</script>

<style scoped>
.section {
  border-radius: 12px !important;
}

.search:focus {
  border: none !important;
  box-shadow: none !important;
}
</style>
<style>
.v-text-field__slot {
  font-size: 13px;
}

.inner-card .section.v-card.v-sheet.theme--dark.elevation-4 {
  background-color: #121212;
}

.v-input__slot {
  margin-bottom: 0px !important;
}

.v-text-field>.v-input__control>.v-input__slot:before {
  border-color: rgb(191, 191, 191);
}
</style>