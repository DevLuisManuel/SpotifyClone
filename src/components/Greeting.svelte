<script lang="ts">
    import {onMount} from 'svelte';

    let greeting = "";

    type GreetingTimes = {
        morning: string;
        afternoon: string;
        night: string;
    };

    type Greetings = {
        [key: string]: GreetingTimes;
    };

    const greetings: Greetings = {
        en: {morning: "Good Morning", afternoon: "Good Afternoon", night: "Good Night"},
        es: {morning: "Buenos Días", afternoon: "Buenas Tardes", night: "Buenas Noches"},
        pt: {morning: "Bom Dia", afternoon: "Boa Tarde", night: "Boa Noite"}
    };

    onMount(() => {
        const currentTime = new Date();
        const currentHour = currentTime.getHours();
        const locale = (navigator.language ?? 'en').slice(0, 2);

        const selectedGreeting = greetings[locale] || greetings['en'];

        if (currentHour < 12) {
            greeting = selectedGreeting.morning;
        } else if (currentHour < 18) {
            greeting = selectedGreeting.afternoon;
        } else {
            greeting = selectedGreeting.night;
        }
    });
</script>

<h1 class="text-3xl font-bold">
    {greeting}
</h1>