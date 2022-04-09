<template>
    <header>
        <h1>Wordle Forever</h1>
        <button class="icon" @click="this.$emit('openHelp')">
            <img alt="Help icon" src="../assets/help.png" height="45" />
        </button>
    </header>
</template>

<script>
export default {
    name: "Header",
};
</script>

<style scoped>
header {
    display: flex;
    justify-content: center;
    border-bottom: 2px solid rgb(52, 52, 52);
    margin: auto;
    margin-bottom: 15px;
    width: 100%;
    max-width: 575px;
}

.icon {
    align-self: stretch;
    display: flex;
    align-items: center;
    margin-left: 15px;
    margin-right: 15px;
    background: none !important;
    border: none !important;
    cursor: pointer;
}
</style>
