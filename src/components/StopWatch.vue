<script setup>
import { ref, computed, watch } from 'vue'
const isWorking = ref(false)
const updating = ref()

const seconds = ref(0)
const minutes = ref(0)
const hours = ref(0)

const showSeconds = computed(() => {
    if (seconds.value < 10)
        return `0${seconds.value}`
    else
        return `${seconds.value}`
})

const showMinutes = computed(() => {
    if (minutes.value === 0 && hours.value === 0)
        return ''
    else if (minutes.value < 10)
        return `0${minutes.value} `
    else return `${minutes.value} `
})

const showHours = computed(() => {
    if (hours.value === 0)
        return ''
    else if (hours.value < 10)
        return `0${hours.value} `
    else return `${hours.value}`
})

const workingClass = computed(() => {
    if (isWorking.value) return 'Stopwatch Working'
    else return 'Stopwatch'
})

const updateTimer = () => {
    if (seconds.value === 59) {
        seconds.value = 0
        if (minutes.value === 59) {
            minutes.value = 0
            hours.value++
        }
        else minutes.value++
    }
    else seconds.value++
}

const resetTimer = () => {
    seconds.value = 0
    minutes.value = 0
    hours.value = 0
    isWorking.value = false
}

watch(
    () => isWorking.value,
    () => {
        if (isWorking.value == true) {
            updating.value = setInterval(updateTimer, 100)
        }
        else clearInterval(updating.value)
    }
)

</script>

<template>
    <div :class="workingClass">
        <div class="Time">
            <span>
                {{ showHours }}
            </span>
            <span v-if="showHours !== ''" class="Separator">
                :
            </span>
            <span>
                {{ showMinutes }}
            </span>
            <span v-if="showMinutes !== ''" class="Separator">
                :
            </span>
            <span>
                {{ showSeconds }}
            </span>
        </div>
        <div class="Buttons">
            <button class="Button" @click="isWorking=!isWorking">
                <span v-if="!isWorking">▶</span>
                <span v-else>||</span>
            </button>
            <button class="Button" @click="resetTimer">
                ■
            </button>
        </div>
    </div>
</template>

<style scoped>

.Stopwatch {
    width: 225px;
    height: 120px;
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background: #696969;
    color: #9E9E9E;
    margin: 10px auto;
}
.Separator {
    margin: 5px;
}
.Working {
    color: white;
}
.Time {
    border-bottom: 1px solid #9E9E9E;
    display: flex;
    height: 50%;
    align-items: center;
    justify-content: center;
}
.Buttons {
    display: flex;
    height: 50%;
    width: 50%;
    margin: 0 auto;
    align-items: center;
    justify-content: space-around;
}
.Button {
    border: none;
    background: none;
    color: inherit;
    cursor: pointer;
}

.Button:hover {
    color: white
}
</style>