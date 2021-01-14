<template>
    <div class="header">
        <div class="review">
            <p>Review</p>
            <div class="star">
                <img src="~/assets/images/staryellow.png" alt="not found">
                <img src="~/assets/images/staryellow.png" alt="not found">
                <img src="~/assets/images/staryellow.png" alt="not found">
                <img src="~/assets/images/staryellow.png" alt="not found">
                <img src="~/assets/images/star.png" alt="not found">
                <!-- <span><i class="fas fa-star"></i></span>
                <span><i class="fas fa-star"></i></span>
                <span><i class="fas fa-star"></i></span>
                <span><i class="fas fa-star"></i></span>
                <span><i class="fas fa-star"></i></span> -->
            </div>
        </div>
        <form>
            <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label"></label>
                <input type="email" class="form-control name" id="exampleInputEmail1" placeholder="Tulis Nama Kamu" >
                <!-- <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div> -->
            </div>
            <div class="form-floating">
                <textarea class="form-control comment" placeholder="Tulis Review Terbaik mu" id="floatingTextarea2" style="height: 80px"></textarea>
                <!-- <label for="floatingTextarea2">Comments</label> -->
            </div>
        </form>
        <div class="button">
            <button type="submit" class="upload">Upload gambar</button>
            <button type="submit" class="send">Kirim</button>
        </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>
    .header {
        padding: 0px 20%;
    }
    .review p {
        font-size: 48px;
        font-weight: 700;
        font-style: normal;
        color: #000000;
        line-height: 56px;
        height: 57px;
    }
    .review {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0px 0px;
    }
    /* .star span i{
        background-color: #E9E22F;
    } */
    form {
        padding: 0px 0px;
        margin-top: -30px;
    }
    .name {
        line-height: 30px;
        background-color: #C4C4C4;
        color: black;
        font-size: 15px;
    }
    .comment {
        background-color: #C4C4C4;
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
    .button .upload {
        background-color: #C4C4C4;
        padding: 5px 20px;
        border: 1px solid #C4C4C4 ;
        color: black;
        font-weight: 400;
    }
    .button .send {
        float: right;
        background-color: #C4C4C4;
        padding: 5px 60px;
        border: 1px solid #C4C4C4 ;
        font-weight: 400;
    }
/* mobile */
    @media(max-width: 678px) {
        .header {
            padding: 20px 20px 0px 20px;
        }
        .review {
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