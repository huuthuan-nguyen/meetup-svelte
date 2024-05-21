<script lang="ts">
    import TextInput from "../UI/TextInput.svelte";
    import Button from "../UI/Button.svelte";
    import {createEventDispatcher} from "svelte";
    import Modal from "../UI/Modal.svelte";

    let title: string = null;
    let subtitle: string = null;
    let address: string = null;
    let email: string = null;
    let description: string = null;
    let imageURL: string = null;

    const dispatch = createEventDispatcher();

    function submitForm(): void {
        dispatch("save", {
            title: title,
            subtitle: subtitle,
            address: address,
            email: email,
            description: description,
            imageURL: imageURL,
        });
    }

    function cancel(): void {
        dispatch("cancel");
    }
</script>
<Modal title="Edit Meetup Data" on:cancel>
    <form on:submit|preventDefault={submitForm}>
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
    </form>
    <div slot="footer">
        <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
        <Button type="submit" on:click={submitForm}>Save</Button>
    </div>
</Modal>

<style>
    form {
        width: 100%;
    }
</style>