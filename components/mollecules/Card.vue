<template>
    <section class="rating">
        <div v-for="(item, index) in dataUser" :key="index" class="rating-user">
            <div style="display:flex">
                <div v-if="item.image.length > 0" class="rating-user-image">
                    <img  :src="item.image" class="rounded-circle" width="60px" alt="not-found">
                </div>
                <div class="rating-user-main">
                    <div class="rating-user-main__name">{{item.name}}</div>
                    <span  id="date" class="rating-user-main__date">{{item.created_at}}</span>
                    <div style="display:flex">
                        <div v-for="(star,id) in starNumber" :key="id" class="rating-main-star" >
                            <img v-if="id+1 <= item.review_star" src="~/assets/images/staryellow.png" alt="not found">
                            <img v-else src="~/assets/images/star.png" alt="">
                        </div>
                    </div>
                    <div class="rating-user-main__content">{{item.review_comment}}</div>
                    <div class="rating-user-main__list">
                        <div class="rating-user-main__list__image">
                            <img :src="item.image" alt="">
                        </div>
                    </div>
                </div>
            </div>
            <div class="dropdown">
                <span class="droplist"><i class="fas fa-ellipsis-h"></i></span>
                <div class="dropdown-content">
                    <a>Edit</a>
                    <a >Delete</a>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import axios from 'axios'
import moment from 'moment'
export default {
     data() {
       return {
           dataUser: [],
           starNumber: 5,
       }
   },
   mounted() {
       this.getDataUser()
   },
   methods: {
       getDataUser() {
           axios.get('https://review-backend.herokuapp.com/api/v1/review')
           .then(res => {
               this.dataUser = res.data.data
               console.log(this.dataUser);
           })
           .catch(err => {
               console.log(err);
           })
       }
   }
}
</script>

<style>
    .rating {
        padding: 0px 20%;
    }
    .rating-user {
        margin-top: 20px;
        display: flex;
        justify-content: space-between;
        padding: 20px 12px 40px;
        background-color: #F5F1F1;
    }
    .rating-user-image {
        margin-right: 10px;
    }
    .rating-user-main__list__image img {
        width: 50px;
        margin: 10px 10px 0px 0px;
        border: 1px solid black;
    }
    .rating-user-main__name {
        font-size: 15px;
    }
    .rating-user-main__date {
        font-size: 14px;
        opacity: 0.5;
    }
    .rating-user-main__content {
        font-size: 15px;
    }
    .droplist {
        opacity: 0.5;
        margin-left: 105px;
        color: black;
        font-size: 16px;
        cursor: pointer;
    }
    .dropdown {
        position: relative;
        display: inline-block;
        text-align: left;
    }
    .dropdown-content {
        border-radius: 20px 0px 20px 20px;
        display: none;
        position: absolute;
        background-color: #C4C4C4;
        width: 115px;
    }
    .dropdown-content a {
        color: black;
        font-weight: 700;
        padding: 2px 14px;
        text-decoration: none;
        display: block;
        cursor: pointer;
    }
    .dropdown-content a:hover {
        background-color: #f1f1f1
    }
    .dropdown:hover .dropdown-content {
        display: block;
    }
    /* .dropdown:hover .droplist {
        background-color: #9facb3a5;
    } */
    @media(max-width: 678px) {
        .rating {
            padding: 0px 20px;
        }
        .rating-user-main__name, .rating-user-main__date,
        .rating-user-main__content {
            font-size: 13px;
        }
        .rating-user-main__list__image img {
            width: 40px;
            margin: 10px 10px 0px 0px;
            border: 1px solid black;
        }
        .rating-user-image img {
            width: 40px;
        }
    }
    @media(max-width: 400px) {
         .dropdown-content  {
             width: 80px;
        }
        .droplist {
            margin-left: 60px;
        }
    }
  
</style>