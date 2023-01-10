<template>

  <ContentBase>
    <div class="row">
      <div class="col-3">
        <UserProfileInfo @follow="follow" @unfollow="unfollow" :user="user" />
        <UserProfileWrite @post_a_post="post_a_post" />
      </div>
      <div class="col-9">
        <UserProfilePosts :posts="posts" />
      </div>
    </div>
  </ContentBase>

</template>

<script>

import ContentBase from '../components/ContentBase';
import UserProfileInfo from '../components/UserProfileInfo';
import UserProfilePosts from '../components/UserProfilePosts';
import UserProfileWrite from '../components/UserProfileWrite';

import {reactive} from 'vue';



export default {
  name: "UserProfile",
  components: {
    ContentBase,
    UserProfileInfo,
    UserProfilePosts,
    UserProfileWrite,
  },
  setup(){
    const user=reactive({
      id: 1,
      username: "保底不歪抽早柚",
      lastName: "Zao",
      firstName: "You",
      followerCount: 0,
      is_followed: false,
    });

    const posts=reactive({
      count: 3,
      posts: [
        {
          id: 1,
          userId: 1,
          content: "今天上web课真开心",
        },
        {
          id: 2,
          userId: 1,
          content: "今天上算法课,更开心了",
        },
        {
          id: 3,
          userId: 1,
          content: "今天上了Acwing,开心极了",
        },
      ]
    });


    const follow=()=>{
      if(user.is_followed)
        return ;
      user.followerCount++;
      user.is_followed=true;
    };

    const unfollow=()=>{
      if(!user.is_followed)
        return ;
      user.followerCount--;
      user.is_followed=false;
    };

    const post_a_post=(content)=>{
      posts.count++;
      posts.posts.unshift({
          id: posts.count,
          userId: 1,
          content: content,
      });
    };

    return{
      user,
      follow,
      unfollow,
      posts,
      post_a_post,
    }
  }
};
</script>



<style scoped>
</style>