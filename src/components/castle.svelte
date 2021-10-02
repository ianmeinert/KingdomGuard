<script>
    import Input from "./input.svelte";
    export let value;

</script>
<Input bind:value={value} type="Castle" path="tech" />