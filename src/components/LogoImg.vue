<template>
    <div class="logo-wrapper">
        <img alt="Your Side" src="@/assets/img/logo.png" />
    </div>
</template>

<script>
export default {
    name: "LogoImg",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.logo-wrapper {
    padding: 30px 0;
    img {
        display: block;
        max-width: 100%;
        margin: auto;
    }
}
</style>
