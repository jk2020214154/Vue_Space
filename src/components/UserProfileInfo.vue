<template>
    <div class="card">
        <div class="card-body">
            <div class="row">
                <div class="col-3">
                    <img class="img-fluid" src="https://cdn.acwing.com/media/user/profile/photo/85276_lg_2de3a67cfe.jpeg" alt="">
                </div>
                <div class="col-9">
                    <div class="username">{{user.username}}</div>
                    <div class="username">{{fullName}}</div>
                    <div class="fans">关注数：{{user.followerCount}}</div>  
                    <button @click="follow" v-if="!user.is_followed" type="button" class="btn btn-success btn-sm">+关注</button>
                    <button @click="unfollow" v-if="user.is_followed" type="button" class="btn btn-danger btn-sm">取消关注</button>
                </div>
            </div>
        </div>
    </div>
</template>


<script>


import {computed} from 'vue';

export default{
    name: "UserProfileInfo",
    props:{
        user:{
            type: Object,
            required: true,
        },
    },
    setup(props,contest){
        let fullName=computed(()=>props.user.lastName+' '+props.user.firstName);
        
        const follow=()=>{
            contest.emit("follow");
        }

        const unfollow=()=>{
            contest.emit("unfollow");
        }
        
        return{
            fullName,
            follow,
            unfollow,
        }
    },
}

</script>


<style scoped>
img{
    border-radius: 50%;
}
.username{
    font-weight: bold;
}

.fans{
    font-size:12px;
    color: gray;
}

button{
    padding:2px 4px;
    font-size: 12px;
}

</style>
