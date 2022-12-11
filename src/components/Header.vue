<template>
    <header>
        <button class="icon" @click="this.$emit('openHelp')">
            <img alt="Help icon" src="../assets/help.png" height="45" />
        </button>
        <h1>Wordle Forever</h1>
    </header>
</template>

<script>
export default {
    name: "Header",
};
</script>

<style scoped>
header {
    border-bottom: 2px solid rgb(52, 52, 52);
    margin: auto;
    margin-bottom: 15px;
    width: 100%;
    max-width: 575px;
    text-align: right;
}

h1 {
    text-align: center;
    position: absolute;
    width: 100%;
    margin: 0;
    top: 13px;
    left: 0;
}

.icon {
    background: none !important;
    border: none !important;
    cursor: pointer;
}
</style>
