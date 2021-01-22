<template>
    <div class="review">
        <div class="review_title">
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
                <input v-model="name" type="email" class="form-control name" id="exampleInputEmail1" placeholder="Tulis Nama Kamu">
            </div>
            <div class="form-floating">
                <textarea v-model="comment" class="form-control comment" placeholder="Tulis Review Terbaik mu" id="floatingTextarea2" style="height: 80px"></textarea>
            </div>
        </form>
        <div class="button">
            <label class="device">
                <span>Upload Gambar</span>
                <input @change="addFile" type="file" id="upload" class="upload">
            </label>
            <button type="submit" class="send" @click.prevent="submitData">Kirim</button>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data() {
        return {
            starNumber: 5,
            choosedRating: 0,
            name: '',
            comment: '',
            add: [],
        }
    },
    methods: {
        addFile(event) {
            let add = (event.target.files);
        },
        // addFile() {
        //     if (this.files && this.files[0]) {

        //         let add = new FileReader()

        //         add.addEventListener('load', function() {
        //             add.readAsDataURL(this.files[0])
        //         })
        //     }
        //     document.getElementById('upload').addEventListener('change', addFile)
        // },
        submitData() {
            const formData = new FormData()
            formData.append("name", this.name)
            formData.append("review_comment", this.comment)
            formData.append("review_star", this.choosedRating)
            formData.append("image", [])
            axios.post('https://review-backend.herokuapp.com/api/v1/review', formData)
            .then(res =>{
                console.log(res);
                console.log('kalau berhasil');
                if (this.choosedRating && this.name && this.comment != '') {
                    this.choosedRating = ''
                    this.name = ''
                    this.comment = ''
                }
                location.reload();
            })
            .catch(err =>{
                console.log(err);
                console.log('kalau gagal');
            })
        }
    }
}
</script>

<style>
    .review {
        padding: 0px 20%;
    }
    .review_title p {
        font-size: 48px;  
        font-weight: 700;
        font-style: normal;
        color: #000000;
        line-height: 56px;
        height: 57px;
    }
    .review_title {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0px 0px;
        cursor: pointer;
    }
    form {
        padding: 0px 0px;
        margin-top: -30px;
    }
    .name {
        line-height: 30px;
        color: black;
        font-size: 15px;
        outline: none;
    }
    .comment {
        margin-top: -10px;
        font-size: 15px;
    }
    .button {
        padding: 0px 0px;
        margin-top: 10px;
    }
    .button::after {
        content: "";
        display: block;
        border: 1px solid black;
        text-align: center;
        width: 100%;
        margin: 30px auto;
    }
    .device {
        background-color: #C4C4C4;
        padding: 5px 20px;
        border: 1px solid #C4C4C4 ;
        font-weight: 400;
        cursor: pointer;
    }
    .device:hover {
        background-color: whitesmoke
    }
    .device input {
        display: none;
    }
    .button .send {
        float: right;
        background-color: #C4C4C4;
        padding: 5px 60px;
        border: 1px solid #C4C4C4 ;
        font-weight: 400;
        outline: none;
    }
    .send:hover {
        background-color: whitesmoke;
    }
/* mobile */
    @media(max-width: 678px) {
        .review {
            padding: 20px 20px 0px 20px;
        }
        .review_title {
            width: 100%;
            padding: 0px 0px;
        }
        form {
            width: 100%;
            padding: 0px 0px;
            margin-top: 10px;
        }
        .name {
            font-size: 14px;
        }
        .comment {
            margin-top: -10px;
            font-size: 14px;
        }
        .button {
            width: 100%;
            padding: 0px 0px;
        }
        .button .upload {
            padding: 5px 10px;
            font-size: 14px;
        }
        .button .send {
            padding: 5px 45px;
            font-size: 14px;
        }
        .button::after {
            content: "";
            display: block;
            border: 1px solid black;
            text-align: center;
            width: 100%;
        }
        .name {
            margin-top: -35px;
        }
    }
</style>