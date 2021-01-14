<template>
<section class="rating">
    <div class="rating-user">
        <div class="rating-user-image">
            <img src="~/assets/images/boy.png" class="rounded-circle" width="60px" alt="not-found">
        </div>
        <div class="rating-user-main">
            <div class="rating-user-main__name">nizammarwadi94@gmail.com</div>
            <span class="rating-user-main__date">02 december 2018</span>
            <div class="rating-main-star">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/star.png" alt="">
            </div>
            <div class="rating-user-main__content">bagus ni broh barangnya, mantaplah</div>
            <div class="rating-user-main__list">
                <div class="rating-user-main__list__image">
                    <img src="~/assets/images/honey.jpg" alt="not-pound">
                    <img src="~/assets/images/honey2.jpg" alt="not-pound">
                    <img src="~/assets/images/honey3.jpg" alt="not-pound">  
                </div>
            </div>
        </div>
    </div>
     <div class="rating-user">
        <div class="rating-user-image">
            <img src="~/assets/images/boy.png" class="rounded-circle" width="60px" alt="not-found">
        </div>
        <div class="rating-user-main">
            <div class="rating-user-main__name">nizammarwadi94@gmail.com</div>
            <span class="rating-user-main__date">02 december 2018</span>
            <div class="rating-main-star">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/star.png" alt="">
            </div>
            <div class="rating-user-main__content">bagus ni broh barangnya, mantaplah</div>
            <div class="rating-user-main__list">
                <div class="rating-user-main__list__image">
                    <img src="~/assets/images/honey3.jpg" alt="not-pound">
                    <img src="~/assets/images/honey.jpg" alt="not-pound">
                    <img src="~/assets/images/honey2.jpg" alt="not-pound">  
                </div>
            </div>
        </div>
    </div>
</section>
    <!-- <section class="ulasam">       
            <div class="image">
                <img src="~/assets/images/staryellow.png" class="image rounded-circle" alt="not-found">
            </div>
            <div class="content">
                <h5 class="title">Afdha</h5>
                <p>2 Desember 2018</p>
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <img src="~/assets/images/staryellow.png" alt="">
                <p class="text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
                <a href="#" class="btn btn-primary">Go somewhere</a>
            </div>
    </section> -->
        <!-- <div class="image" style="width: 18rem;">
            <img src="~assets/images/star.png" class="card-img-top" alt="not-found">
        </div>
        <div class="card-content">
            <h5 class="card-title">Card title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div> -->
</template>

<script>
export default {

}
</script>

<style>
    .rating {
        padding: 0px 20%;
        margin-top: -20px;
    }
    .rating-user {
        margin-top: 20px;
        display: flex;
        padding: 20px 12px 40px;
        /* width: 672px;
        margin: 0px auto;
        padding: 0px 12px; */
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
</style>