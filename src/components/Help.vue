<template>
  <div class="help-backdrop">
    <div class="help-modal">
      <h1>How to Play</h1>
      <div class="help-info">
        Guess the <b>WORDLE</b> in 6 tries.
        <br />
        <br />
        After each guess, the colour of the tiles will change to show how close
        your guess was to the wordle.
        <br />
        <br />
        Green indicates the letter is in the correct spot. Yellow indicates the
        letter is in the wordle but in the incorrect spot. Grey indicates the
        letter is not in the wordle.
        <br />
        <br />
        This is an infinite version of
        <a href="https://www.powerlanguage.co.uk/wordle/">Wordle</a>.
      </div>
      <button class="button" @click="this.$emit('closeHelp')">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Help",
};
</script>

<style scoped>
.help-modal {
  background-color: rgb(32, 32, 32);
  width: 100%;
  max-width: 445px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.help-info {
  text-align: left;
  text-transform: none;
  font-weight: normal;
  letter-spacing: normal;
  margin-left: 15px;
  margin-right: 15px;
  margin-bottom: 10px;
}

.help-backdrop {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>