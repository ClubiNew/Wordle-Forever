<template>
    <header>
        <div class="spacer"></div>
        <h1>Wordle Forever</h1>
        <button class="icon" @click="this.$emit('openHelp')">
            <img alt="Help icon" src="help.png" height="45" />
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
    justify-content: space-around;
    border-bottom: 2px solid rgb(52, 52, 52);
    margin: auto;
    margin-bottom: 15px;
    width: 100%;
    max-width: 575px;
    text-align: center;
}

.spacer {
    width: 45px;
}

.icon {
    padding: 0;
    background: none !important;
    border: none !important;
    cursor: pointer;
}
</style>
