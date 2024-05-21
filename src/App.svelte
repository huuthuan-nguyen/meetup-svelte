<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import TextInput from "./UI/TextInput.svelte";
    import Button from "./UI/Button.svelte";

    let title = "";
    let subtitle = "";
    let address = "";
    let email = "";
    let description = "";
    let imageURL = "";

    let meetups = [
        {
            id: "m1",
            title: "Coding Bootcamp",
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
            subtitle: "Let's go for some swimming",
            description: "We will simply swim some rounds",
            imageURL:
                "https://upload.wikimedia.org/wikipedia/commons/1/10/Hanoi_Skyline_-_NKS.jpg",
            address: "Ha Noi, Vietnam",
            contactEmail: "swim@test.com",
        },
    ];

    function addMeetup() {
        const newMeetup = {
            id: Math.random().toString(),
            title: title,
            subtitle: subtitle,
            description: description,
            imageURL: imageURL,
            contactEmail: email,
            address: address,
        };

        meetups = [...meetups, newMeetup];
    }
</script>

<Header />

<main>
    <form on:submit|preventDefault={addMeetup}>
        <TextInput
            controlType="input"
            label="Title"
            id="title"
            value={title}
            on:input={(event) => (title = event.target.value)}
        />
        <TextInput
            controlType="input"
            label="Subtitle"
            id="subtitle"
            value={subtitle}
            on:input={(event) => (subtitle = event.target.value)}
        />
        <TextInput
            controlType="input"
            label="Address"
            id="address"
            value={address}
            on:input={(event) => (address = event.target.value)}
        />
        <TextInput
            controlType="input"
            label="Image URL"
            id="imageURL"
            value={imageURL}
            on:input={(event) => (imageURL = event.target.value)}
        />
        <TextInput
            controlType="input"
            type="email"
            label="Email"
            id="email"
            value={email}
            on:input={(event) => (email = event.target.value)}
        />
        <TextInput
            controlType="textarea"
            label="Description"
            id="description"
            value={description}
            on:input={(event) => (description = event.target.value)}
        />
        <Button type="submit" caption="Save" />
    </form>
    <MeetupGrid {meetups} />
</main>

<style>
    main {
        margin-top: 5rem;
    }

    form {
        width: 30rem;
        max-width: 90%;
        margin: auto;
    }
</style>
