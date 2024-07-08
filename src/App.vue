<template>
    <div class="container">
        <LogoImg></LogoImg>
        <FiltersBar
            :products="products"
            @update:selected-styles="updateSelectedStyles"
        ></FiltersBar>
        <div class="wrapper">
            <MirrorsList
                :products="products"
                :selectedStyles="selectedStyles"
                :cartProducts="cartProducts"
                @add-to-cart="addToCart"
                @increase-quantity="increaseQuantity"
                @decrease-quantity="decreaseQuantity"
            ></MirrorsList>
            <ShopCart :cartProducts="cartProducts"></ShopCart>
        </div>
    </div>
</template>

<script>
import products from "@/assets/products.json";
import FiltersBar from "./components/FiltersBar.vue";
import LogoImg from "./components/LogoImg.vue";
import MirrorsList from "./components/MirrorsList.vue";
import ShopCart from "./components/ShopCart.vue";

export default {
    name: "App",
    components: {
        LogoImg,
        FiltersBar,
        MirrorsList,
        ShopCart,
    },
    data() {
        return {
            products: products,
            selectedStyles: [],
            cartProducts: [],
        };
    },
    methods: {
        updateSelectedStyles(styles) {
            this.selectedStyles = styles;
        },
        addToCart(product) {
            const index = this.cartProducts.findIndex(
                (item) => item.id === product.id
            );
            if (index !== -1) {
                this.cartProducts[index].quantity++;
            } else {
                this.cartProducts.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    quantity: 1,
                });
            }
        },
        increaseQuantity(productId) {
            const index = this.cartProducts.findIndex(
                (item) => item.id === productId
            );
            if (index !== -1) {
                this.cartProducts[index].quantity++;
            }
        },
        decreaseQuantity(productId) {
            const index = this.cartProducts.findIndex(
                (item) => item.id === productId
            );
            if (index !== -1) {
                this.cartProducts[index].quantity--;
                if (this.cartProducts[index].quantity === 0) {
                    this.cartProducts.splice(index, 1);
                }
            }
        },
    },
};
</script>

<style lang="scss">
html {
    overflow-y: scroll;

    ::-webkit-scrollbar {
        width: 8px;
        background-color: #e9c7b5;
    }

    /* Esquinas redondeadas */
    ::-webkit-scrollbar-thumb {
        border-radius: 10px;
        background-color: #d3a68a;
    }

    /* Cambiar color al pasar el mouse */
    ::-webkit-scrollbar-thumb:hover {
        background-color: #c99b7e;
    }
}

body {
    background-color: #e9e2de;
}

#app {
    font-family: Roboto, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

.container {
    display: block;
    margin: auto;
    width: 960px;
}

ul {
    margin: 0;
    padding: 0;
    list-style: none;
}

button {
    background-color: transparent;
    border: none;
    padding: 0;
}

.wrapper {
    display: flex;
    gap: 40px;
    margin-top: 40px;
}
</style>
