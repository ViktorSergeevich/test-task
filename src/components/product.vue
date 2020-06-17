<template>
    <div class="product product_horizontal">                  <!-- product_horizontal-->
        <span class="product_code">Код: {{product_data.code}}</span>
        <div class="product_status_tooltip_container">
            <span class="product_status">Наличие</span>
        </div>                                
        <div class="product_photo">
            <a href="#" class="url--link product__link">
                <!-- <img src="misc/df126-52f2-11e5-b9a9-00259036a192_220x220_1.jpg"> -->
                <img :src="addModify(product_data.primaryImageUrl)">
            </a>                                    
        </div>
        <div class="product_description">
            <a href="#" class="product__link"> {{product_data.title}} </a>
        </div>
        <div class="product_tags hidden-sm">
            <p>Могут понадобиться:</p>
            <!-- <a href="#" class="url--link">{{product_data.assocProducts.split(\n)}}</a> -->
            <a href="#" class="url--link">плинтус натуральный,</a>
            <a href="#" class="url--link">рулетка,</a>
            <a href="#" class="url--link">набор для укладки ламината,</a>
            <a href="#" class="url--link">ножовка по ламинату,</a>
            <a href="#" class="url--link">гель для стыков ламината Clic Protect.</a>
        </div>
        <div class="product_units">
            <div class="unit--wrapper">
                <div class="unit--select" :class="{ 'unit--active' : this.metr }" @click="changeMetr">
                    <p class="ng-binding">За м. кв.</p>
                </div>
                <div class="unit--select" :class="{ 'unit--active' : this.pack }" @click="changePack">
                    <p class="ng-binding">За упаковку</p>
                </div>
            </div>
        </div>
        <p class="product_price_club_card">
            <span class="product_price_club_card_text">По карте<br>клуба</span>
            <span class="goldPrice"> {{calcPriceCart(product_data.priceGold, product_data.priceGoldAlt)}}</span>
            <span class="rouble__i black__i">
                <svg version="1.0" id="rouble__b" xmlns="http://www.w3.org/2000/svg" x="0" y="0" width="30px" height="22px" viewBox="0 0 50 50" enable-background="new 0 0 50 50" xml:space="preserve">
                    <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#rouble_black"></use>
                </svg>
                </span>
        </p>
        <p class="product_price_default">
            <span class="retailPrice"> {{calcPriceCart(product_data.priceRetail, product_data.priceRetailAlt)}} </span>
            <span class="rouble__i black__i">
                <svg version="1.0" id="rouble__g" xmlns="http://www.w3.org/2000/svg" x="0" y="0" width="30px" height="22px" viewBox="0 0 50 50" enable-background="new 0 0 50 50" xml:space="preserve">
                    <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#rouble_gray"></use>
                </svg>
                </span>
        </p>
        <div class="product_price_points">
            <p class="ng-binding">Можно купить за 231,75 балла</p>
        </div>
        <div class="list--unit-padd"></div>
        <div class="list--unit-desc">
            <div class="unit--info">
                <div class="unit--desc-i"></div>
                <div class="unit--desc-t">
                    <p>
                        <span class="ng-binding">Продается упаковками:</span>
                        <span class="unit--infoInn">{{product_data.unitRatio}} {{product_data.unit}} 
                            = {{product_data.unitRatioAlt.toFixed(2)}} {{product_data.unitAlt}} </span>
                    </p>
                </div>
            </div>
        </div>
        <div class="product__wrapper">
            <div class="product_count_wrapper">
                <div class="stepper">
                    <input class="product__count stepper-input" type="text" v-model="counter">   
                    <span class="stepper-arrow up" @click="incCounter"></span>
                    <span class="stepper-arrow down" @click="decCounter"></span>                                            
                </div>
            </div>
            <span class="btn btn_cart" data-url="/cart/" :data-product-id="product_data.productId">
                <!-- <svg class="ic ic_cart">
                    <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#cart"></use>
                </svg> -->
                <span class="cart"></span>
                <span class="ng-binding">В корзину</span>
            </span>
        </div>
    </div>
</template>

<script>

export default {
    name: 'product',
    props: {
        product_data: {
            type: Object,
            default(){
                return {}
            } 
        }
    }, 
    data() {
        return {
            counter: 1,
            pack: false,
            metr: true,
        }
    },
    methods: {
        addModify(string){
            let str = string.split('').reverse().join('')
            let exp = str.split('.')[0] +'.'
            let text = str.split('.')[1] + '.'
            let site = str.split('.')[2] 
            let output = exp + '1_022x022_' + text + site
            return output.split('').reverse().join('')
        },
        incCounter(){
           return this.counter++
        },
        decCounter(){   
            if(this.counter > 1)
                return this.counter--
        },
        changeValue(){
            console.log(this)
        },
        changePack(){
            this.pack = true
            this.metr = false
        },
        changeMetr(){
            this.pack = false
            this.metr = true
        },
        calcPriceCart(gold, goldAlt){
            if(this.metr)
                return (goldAlt * this.counter).toFixed(2)
            else
                return (gold * this.counter).toFixed(2)
        },
        calcPrice(retail, retailAlt){
            if(this.metr)
                return (retailAlt * this.counter).toFixed(2)
            else
                return (retail * this.counter).toFixed(2)
        }
    }
}

</script>

<style>

</style>