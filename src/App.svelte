<script lang="ts">
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import EditMeetup from "./Meetups/EditMeetup.svelte";
    import Button from "./UI/Button.svelte";

    let meetups = [
        {
            id: "m1",
            title: "Coding Bootcamp",
            isFavourite: false,
            subtitle: "Learn to code in 2 hours",
            description:
                "In this meetup, we will have some experts that teach you how to code!",
            imageURL:
                "https://upload.wikimedia.org/wikipedia/commons/1/10/Hanoi_Skyline_-_NKS.jpg",
            address: "Ha Noi, Vietnam",
            contactEmail: "code@test.com",
        },
        {
            id: "m2",
            title: "Swim Together",
            isFavourite: false,
            subtitle: "Let's go for some swimming",
            description: "We will simply swim some rounds",
            imageURL:
                "https://upload.wikimedia.org/wikipedia/commons/1/10/Hanoi_Skyline_-_NKS.jpg",
            address: "Ha Noi, Vietnam",
            contactEmail: "swim@test.com",
        },
    ];

    let editMode: string;

    function addMeetup(event) {
        const newMeetup = {
            id: Math.random().toString(),
            title: event.detail.title,
            isFavourite: false,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            imageURL: event.detail.imageURL,
            contactEmail: event.detail.email,
            address: event.detail.address,
        };

        meetups = [...meetups, newMeetup];
        editMode = null;
    }

    function toggleFavourite(event) {
        const id = event.detail;
        const updatedMeetup = {...meetups.find(m => m.id === id)};
        updatedMeetup.isFavourite = !updatedMeetup.isFavourite;
        const meetupIndex = meetups.findIndex(m => m.id === id);
        const updatedMeetups = [...meetups];
        updatedMeetups[meetupIndex] = updatedMeetup;
        meetups = updatedMeetups;
    }

    function cancelEdit(): void {
        editMode = null;
    }
</script>

<Header/>

<main>
    <div class="meetup-controls">
        <Button on:click={() => editMode = "add"}>New Meetup</Button>
    </div>
    {#if editMode === "add"}
        <EditMeetup on:save={addMeetup} on:cancel={cancelEdit}/>
    {/if}
    <MeetupGrid {meetups} on:toggleFavourite={toggleFavourite}/>
</main>

<style>
    main {
        margin-top: 5rem;
    }

    .meetup-controls {
        margin: 1rem;
    }
</style>
