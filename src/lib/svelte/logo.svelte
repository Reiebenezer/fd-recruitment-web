<script lang="ts">
    import logo from '$lib/assets/logo.svg';
    import logoblue from '$lib/assets/logo_blue.svg';

    export let type: 'blue' | 'white' = 'white';
</script>

<span><img src="{type === 'blue' ? logoblue : logo}" alt="FD Logo"></span>

<style lang="scss">
    span {
        width: 5rem;
        height: 5rem;

        display: inline-flex;
    }

    img {
        max-width: 100%;
        object-fit: contain;
    }
</style>