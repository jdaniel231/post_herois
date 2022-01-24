<template>
  <v-container>
    <v-alert
      border="left"
      color="green"
      close-text="Close Alert"
      dark
      dismissible
      v-if="this.$route.params.message"
    > {{this.$route.params.message}} 
    </v-alert>
    <v-row no-gutters >
      <v-col sm="4" class="pa-3" v-for="post in posts" :key="post._id" >
        <v-card class="pa-1">
          <v-img height="250" :src="`/${post.image}`"></v-img>
          <v-row class="mt-1 mx-1">
            <v-col sm="2">
              <v-btn small outlined color="indigo" >
                {{ post.category }}
              </v-btn>
            </v-col>
            <v-col sm="10" class=" d-flex justify-end">
              <v-btn  text icon color="blue" :to="{name: 'post', params: {id: post._id}}">
                <v-icon>mdi-eye</v-icon>
              </v-btn>                        
              <!-- <v-btn color="red" text icon @click="removePost(post._id)" >
                  <v-icon>mdi-delete</v-icon>
              </v-btn> -->
            </v-col>
            
          </v-row>          
          <v-card-title class="headline" >
            {{ post.title }}
          </v-card-title>
          <v-card-text class="py-0" >
            <p> {{post.content.substring(0, 100) + "..."}} </p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import API from '../api';

  export default {
    name: 'Home',
    data() {
      return{
        posts: [],
      };
    },

    async created() {
      this.posts = await API.getAllPost();
    },
    // methods: {
    //   async removePost(id) {
    //     const response = await API.deletePost(id);
    //     this.$router.push({ name: 'home', params: {message: response.message}})
    //   }
    // }

   
  };
</script>
