<template>
    <div class="shop-cart">
        <h2>Cart</h2>
        <div class="price-table">
            <div v-for="item in cartProducts" :key="item.id" class="line">
                <div class="title">
                    <div class="qty">{{ item.quantity }}</div>
                    <div class="name">{{ item.name }}</div>
                </div>
                <div class="price">{{ item.price * item.quantity }}</div>
            </div>
        </div>
        <div class="total-price">
            <div class="title">Total:</div>
            <div class="price">{{ calculateTotalPrice }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ShopCart",
    props: {
        cartProducts: {
            type: Array,
            required: true,
        },
    },
    computed: {
        calculateTotalPrice() {
            return this.cartProducts.reduce((total, item) => {
                return total + item.price * item.quantity;
            }, 0);
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.shop-cart {
    width: 25%;
    padding: 20px;
    background-color: #e7c8b8;
    border-radius: 4px;
    height: fit-content;
    h2 {
        color: #5f402c;
        margin: 0;
    }
    .price-table {
        display: flex;
        flex-direction: column;
        gap: 10px;
        margin-top: 20px;
        .line {
            display: flex;
            justify-content: space-between;
            color: #5f402c;
            .title {
                display: flex;
                .qty {
                    &:after {
                        content: "x";
                        display: inline-block;
                        margin: 0 1px;
                    }
                }
                .name {
                    margin-left: 2px;
                }
            }
        }
        .price {
            &:before {
                content: "$";
                display: inline-block;
                margin: 0 1px;
            }
        }
    }
    .total-price {
        position: relative;
        display: flex;
        justify-content: space-between;
        width: 100%;
        margin-top: 15px;
        font-size: 20px;
        font-weight: 500;
        color: #5f402c;
        &:before {
            content: "";
            position: absolute;
            width: 100%;
            top: -5px;
            left: 0;
            right: 0;
            height: 1px;
            background-color: #5f402c;
        }
        .price {
            color: #5f402c;
            &:before {
                content: "$";
                display: inline-block;
                margin: 0 1px;
                color: #5f402c;
            }
        }
    }
}
</style>
