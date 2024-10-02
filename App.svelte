<script>
    import "@picocss/pico";

    import toast, { Toaster } from "svelte-french-toast";
</script>

<Toaster />
<main class="container">
    <hgroup>
        <h1>parcel-resolver-exports-bug</h1>
        <p><em>Is</em> this even a bug?</p>
    </hgroup>

    <p>Click to vote!</p>
    <button on:click={() => toast.success("Of course it's a bug!")}>
        Yes!
    </button>
    <button on:click={() => toast.error("Learn configuration properly!")}>
        No...
    </button>
</main>
