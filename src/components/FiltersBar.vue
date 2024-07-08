<template>
    <ul>
        <li
            v-for="(style, index) in styles"
            :key="index"
            :class="{ selected: isSelected(style) }"
            @click="toggleStyle(style)"
        >
            {{ style }}
        </li>
    </ul>
</template>

<script>
export default {
    name: "FiltersBar",
    props: {
        products: {
            type: Array,
            required: true,
        },
    },
    data() {
        return {
            selectedStyles: [],
        };
    },
    computed: {
        styles() {
            const styles = new Set();
            this.products.forEach((product) => {
                styles.add(product.style);
            });
            return Array.from(styles);
        },
    },
    methods: {
        toggleStyle(style) {
            const index = this.selectedStyles.indexOf(style);
            if (index === -1) {
                this.selectedStyles.push(style);
            } else {
                this.selectedStyles.splice(index, 1);
            }
            this.$emit("update:selected-styles", this.selectedStyles);
        },
        isSelected(style) {
            return this.selectedStyles.includes(style);
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul {
    display: flex;
    max-width: 400px;
    justify-content: center;
    gap: 10px;
    margin: auto;
    flex-wrap: wrap;

    li {
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 12px;
        font-weight: 600;
        color: #7a553e;
        border: solid 1px #cea893;
        border-radius: 4px;
        padding: 4px 15px;
        text-transform: uppercase;
        transition: 0.3s;
        cursor: pointer;
        &:hover {
            transform: translateY(-3px);
        }
        &.selected {
            background-color: #7a553e;
            border-color: #7a553e;
            color: #fff;
        }
    }
}
</style>
