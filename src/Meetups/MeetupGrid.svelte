<script>
    import MeetupItem from "./MeetupItem.svelte";

    export let meetups;
</script>

<section id="meetups">
    {#each meetups as meetup, index (meetup.id)}
        <MeetupItem
                id={meetup.id}
                title={meetup.title}
                isFavourite={meetup.isFavourite}
                subtitle={meetup.subtitle}
                imageURL={meetup.imageURL}
                description={meetup.description}
                address={meetup.address}
                contactEmail={meetup.contactEmail}
                on:toggleFavourite
        />
    {/each}
</section>

<style>
    section {
        width: 100%;
        display: grid;
        grid-template-columns: 1fr;
        grid-gap: 1rem;
    }

    @media (min-width: 768px) {
        section {
            grid-template-columns: repeat(2, 1fr);
        }
    }
</style>
