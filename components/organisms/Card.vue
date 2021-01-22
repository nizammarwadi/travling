<template>
    <div>
        <div class="modal" tabindex="-1" style="display: block" v-if="isEditting">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="form-edit"  >
                        <div class="review">
                            <p>Review</p>
                            <div style="display:flex">
                                <div v-for="(star,id) in starNumber" :key="id" class="star" id="star">
                                    <img v-if="id+1 <= choosedRating" @click="choosedRating = id+1" src="~/assets/images/staryellow.png" alt="not found">
                                    <img v-else @click="choosedRating = id+1" src="~/assets/images/star.png" alt="">
                                </div>
                            </div>
                        </div>
                        <form>
                            <div class="mb-3">
                                <label for="name" class="form-label"></label>
                                <input v-model="choosedName" type="email" class="form-control name" id="exampleInputEmail1" placeholder="Tulis Nama Kamu">
                            </div>
                            <div class="form-floating">
                                <textarea v-model="choosedComment" class="form-control comment" placeholder="Tulis Review Terbaik mu" id="floatingTextarea2" style="height: 80px"></textarea>
                            </div>
                        </form>
                        <div class="button">
                            <label class="device">
                                <span>Upload Gambar</span>
                                <input @change="addFile" type="file" id="upload" class="upload">
                            </label>
                            <button type="submit" class="send" @click.prevent="submitEditData">Kirim</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <section class="rating">
            <div v-for="(item, index) in dataUser" :key="index" class="rating-user">
                <div style="display:flex">
                    <div class="rating-user-image">
                        <img :src="imgUser" class="rounded-circle" width="40px" alt="">
                    </div>
                    <div class="rating-user-main">
                        <div class="rating-user-main__name">{{item.name}}</div>

                        <span  id="date" class="rating-user-main__date">{{ convertToDate(item.created_at) }}</span>

                        <div style="display:flex">
                            <div v-for="(star,id) in starNumber" :key="id" class="rating-main-star" >
                                <img v-if="id+1 <= item.review_star" src="~/assets/images/staryellow.png" alt="not found">
                                <img v-else src="~/assets/images/star.png" alt="">
                            </div>
                        </div>
                        <div class="rating-user-main__content">{{item.review_comment}}</div>
                        <div class="rating-user-main__list">
                            <div class="rating-user-main__list__image" v-for="(img, imgId) in item.image" :key="imgId">
                                <img :src="`data:image/png;base64, ${img.b64}`" :alt="img.originalName">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="dropdown">
                    <span class="droplist"><i class="fas fa-ellipsis-h"></i></span>
                    <div class="dropdown-content">
                        <a @click="clickEdit(item)">Edit</a>
                        <a @click="deleteDataUser(item)">Delete</a>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>
<script>
import axios from 'axios'
import moment from 'moment'
export default {
    data() {
        return {
            dataUser: [],
            starNumber: 5,
            imgUser: "data:image/png;base64,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",
            choosedId: '',
            choosedRating: '',
            isEditting: false,
            choosedName: '',
            choosedComment: '',
            created_at: '',
            choosedImg: []
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
                console.log(dataUser);
            })
            .catch(err => {
                console.log(err);
            })
        },
        convertToDate(value) {
            return moment(value).format('DD MMMM YYYY')
        },
        clickEdit(item) {
            this.isEditting = true
            this.choosedId = item._id
            this.choosedName = item.name
            this.choosedComment = item.review_comment,
            this.choosedRating = item.review_star
            this.choosedImg = item.image
            console.log(this.choosedImg);
        },
        addFile() {

        },
        submitEditData() {
            const formData = new FormData()
            formData.append("name", this.choosedName)
            formData.append("review_comment", this.choosedComment)
            formData.append("review_star", this.choosedRating)
            formData.append("image", this.choosedImg)
            axios.put(`https://review-backend.herokuapp.com/api/v1/review/${this.choosedId}`, formData)
            .then(res => {
                this.dataUser = res.data.data
                console.log(this.dataUser);
                this.isEditting = false
            })
            .catch(err => {
                console.log(err);
            })
        },
        deleteDataUser(item) {
            axios.delete(`https://review-backend.herokuapp.com/api/v1/review/${item._id}`,)
            .then(res => {
                console.log(res);
                this.getDataUser()
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
    .rating-user-main__list {
        display: flex;
    }
    .rating-user-main__list__image img {
        width: 50px;
        margin: 10px 10px 0px 0px;
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