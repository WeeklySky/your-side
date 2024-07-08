<template>
    <ul>
        <li v-for="product in filteredProducts" :key="product.id">
            <div class="mirror-img">
                <img
                    :src="require(`@/assets/img/mirrors/${product.image}`)"
                    alt=""
                />
            </div>
            <div class="content">
                <div class="info">
                    <div class="title">{{ product.name }}</div>
                    <div class="price">{{ product.price }}</div>
                </div>
                <div class="buy-action">
                    <button
                        v-if="!productInCart(product.id)"
                        @click="addToCart(product)"
                    >
                        Buy
                    </button>
                    <div v-if="productInCart(product.id)" class="item-qty">
                        <button
                            class="btn-qty"
                            @click="decreaseQuantity(product.id)"
                        >
                            -
                        </button>
                        <div class="qty">
                            {{ getProductQuantity(product.id) }}
                        </div>
                        <button
                            class="btn-qty"
                            @click="increaseQuantity(product.id)"
                        >
                            +
                        </button>
                    </div>
                </div>
            </div>
        </li>
    </ul>
</template>

<script>
export default {
    name: "MirrorsList",
    props: {
        products: {
            type: Array,
            required: true,
        },
        selectedStyles: {
            type: Array,
            required: true,
        },
        cartProducts: {
            type: Array,
            required: true,
        },
    },
    computed: {
        filteredProducts() {
            if (this.selectedStyles.length === 0) {
                return this.products;
            } else {
                return this.products.filter((product) =>
                    this.selectedStyles.includes(product.style)
                );
            }
        },
    },
    methods: {
        addToCart(product) {
            this.$emit("add-to-cart", product);
        },
        productInCart(productId) {
            return this.cartProducts.some((item) => item.id === productId);
        },
        getProductQuantity(productId) {
            const cartItem = this.cartProducts.find(
                (item) => item.id === productId
            );
            return cartItem ? cartItem.quantity : 0;
        },
        increaseQuantity(productId) {
            this.$emit("increase-quantity", productId);
        },
        decreaseQuantity(productId) {
            this.$emit("decrease-quantity", productId);
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    width: calc(70% - 20px);

    li {
        box-sizing: border-box;
        width: calc((100% - 40px) / 3);
        padding: 15px;
        border: solid 1px #cea893;
        border-radius: 4px;
        .mirror-img {
            display: flex;
            object-fit: cover;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            height: 260px;
            img {
                border-radius: 4px;
                max-width: 100%;
                height: auto;
            }
        }
        .content {
            display: flex;
            justify-content: space-between;
            margin-top: 15px;
            .info {
                .title {
                    font-size: 14px;
                }
                .price {
                    font-size: 14px;
                    font-weight: 700;
                    margin-top: 5px;
                }
            }
            button {
                font-family: "Roboto";
                background-color: #2a7d55;
                display: block;
                height: fit-content;
                padding: 5px 15px;
                border-radius: 30px;
                color: #fff;
                text-transform: uppercase;
                font-size: 12px;
                font-weight: 700;
                letter-spacing: 1px;
                transition: 0.2s;
                &:hover {
                    background-color: #51bb88;
                }
            }
            .buy-action {
                .item-qty {
                    display: flex;
                    .btn-qty {
                        background-color: rgb(224, 214, 199);
                        padding: 3px 6px;
                        color: #7e6152;
                    }
                    .qty {
                        margin: 0 5px;
                        font-size: 16px;
                    }
                }
            }
        }
    }
}
</style>
