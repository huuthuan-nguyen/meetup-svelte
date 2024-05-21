<script lang="ts">
    import Button from "../UI/Button.svelte";
    import {createEventDispatcher} from "svelte";
    import Badge from "../UI/Badge.svelte";

    export let title: string;
    export let subtitle: string;
    export let imageURL: string;
    export let description: string;
    export let address: string;
    export let contactEmail: string;
    export let id: string;
    export let isFavourite: boolean = false;

    const dispatch = createEventDispatcher();
</script>

<article>
    <header>
        <h1>
            {title}
            {#if isFavourite}
                <Badge>FAVOURITE</Badge>
            {/if}
        </h1>
        <h2>{subtitle}</h2>
        <p>{address}</p>
    </header>
    <div class="image">
        <img src={imageURL} alt={title}/>
    </div>
    <div class="content">
        <p>{description}</p>
    </div>
    <footer>
        <Button href="mailto:{contactEmail}" caption="Contact" type="link"/>
        <Button
                type="button"
                caption={isFavourite ? "Unfavourite" : "Favourite"}
                mode="outline"
                color={isFavourite ? null : "success"}
                on:click={() => dispatch("toggleFavourite", id)}
        />
        <Button type="button" caption="Show Details"/>
    </footer>
</article>

<style>
    article {
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
        border-radius: 5px;
        background: white;
        margin: 1rem;
    }

    header,
    .content,
    footer {
        padding: 1rem;
    }

    .image {
        width: 100%;
        height: 14rem;
    }

    .image img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    h1 {
        font-size: 1.25rem;
        margin: 0.5rem 0;
        font-family: "Roboto Slab", sans-serif;
    }

    h1.is-favorite {
        background: #01a129;
        color: white;
        padding: 0 0.5rem;
        border-radius: 5px;
    }

    h2 {
        font-size: 1rem;
        color: #808080;
        margin: 0.5rem 0;
    }

    p {
        font-size: 1.25rem;
        margin: 0;
    }

    div {
        text-align: right;
    }

    .content {
        height: 4rem;
    }
</style>
