<template>
    <form>
        <label for="min">Minuty<br/>
            <input type="number" v-model="minutes" name="time_m" id="min" min="0" max="59">
        </label>
        <label for="sec">Sekundy<br/>
            <input type="number" v-model="seconds" name="time_s" id="sec" max="59" min="0">
        </label>
        <button type="button" class="setButton" @click="setTime">Ustaw czas</button>
    </form>
</template>

<script lang="ts">
import { Component, Vue, Emit} from 'vue-property-decorator';

@Component({})
export default class TimerSetup extends Vue {
    minutes: number = 0;
    seconds: number = 0;

    @Emit()
    setTime(): {minutes: number; seconds: number} {
        return {minutes: this.minutes, seconds: this.seconds}
    }
}
</script>