<script>
    export let bindData;
    import LoremImpsum from "../components/seeds/LoremImpsum.svelte"
    let toParent = {
        title:"Beranda"
    };
    if ('function' === typeof bindData) {
        // Pass input value to the top
        bindData(toParent);
    }
</script>
<LoremImpsum />