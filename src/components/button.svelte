<script>
    export let styles = '';
</script>

<style lang="scss">
    .form-button {
        font-size: 18px;
        font-weight: 400;
        color: #FFFFFFB2;
        padding: 11px 40px;
        border-radius: 50px;
        border: none;
        transition: 0.3s;
        cursor: pointer;
        &:hover {
            background-color: #404463;
        }
    }
</style>

<button style={styles} class="form-button" type="submit">Send</button>