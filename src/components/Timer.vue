<template>
    <div class="timer">{{ time|transform }}</div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({
    filters: {
        transform(value: string): string {
            let data = value.split(':');
            let minutes = data[0];
            let seconds = data[1];
            if (parseInt(minutes) < 10) {
                minutes = "0" + minutes;
            }
            if (parseInt(seconds) < 10) {
                seconds = "0" + seconds;
            }
            return minutes + ":" + seconds;
        }
    }
})
export default class TimerSetup extends Vue {
    @Prop(Number) private time!: number;
}
</script>