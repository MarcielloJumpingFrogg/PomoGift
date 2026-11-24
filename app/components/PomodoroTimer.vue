<script setup lang="ts">

const pomoSeconds = ref(0);
const defaultPomoMinutes = ref(25);
const pomoMinutes = ref(defaultPomoMinutes.value);
const pause = ref(true);

function resetTimer() {
  pomoMinutes.value = defaultPomoMinutes.value;
  pomoSeconds.value = 0;
	pause.value = true
	toggleTimer()
}

function toggleTimer() {
	pause.value = !pause.value
}

async function timer() {
  while ((pomoSeconds.value > 0 || pomoMinutes.value > 0) && pause.value == false) {
    if (pomoSeconds.value == 0) {
      pomoMinutes.value -= 1;
      pomoSeconds.value = 59;
    } else if (pomoSeconds.value > 0) {
      pomoSeconds.value--;
    }
    await new Promise((r) => setTimeout(r, 1000));
  }
  resetTimer();
}


onMounted(async () => {
  watch(pause, async () => {
    await timer();
  });
});
</script>

<template>
  <label for="PomodorMinutes">Minutes: </label>
  <input
    type="number"
    v-model.lazy="defaultPomoMinutes"
    id="PomodorMinutes"
    @keyup.prevent.enter="resetTimer()"
  />

  <div>
		<h1>{{ pomoMinutes >= 0 ? String(pomoMinutes).padStart(2, "0") : "00" }}:{{ String(pomoSeconds).padStart(2, "0") }}</h1>
    <button @click.prevent="resetTimer()">Start</button>
  </div>
</template>
