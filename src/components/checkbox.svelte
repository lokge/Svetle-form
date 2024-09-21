<script>
    import { onMount } from 'svelte';

    export let registerInput;

    let mainCheckbox;
    let errorMessage = '';
    let isValid = true;

    onMount(() => {
        if (registerInput) {
            registerInput({ 
                element: mainCheckbox, 
                checkValidity: checkValidity 
            });
        }
    });

    function checkValidity() {
        isValid = true;
        errorMessage = '';

        console.log(mainCheckbox.checked);
        if (!mainCheckbox.checked) {
            isValid = false;
        }

        return isValid;
    }

    function onClick(event) {
        if (event.target.classList.contains('error')) {
            event.target.classList.remove('error');
            isValid = true;
            errorMessage = '';
        }
    }
</script>

<style lang="scss">
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: 'Roboto', sans-serif;
    }
    .checkbox {
        width: 26px;
        height: 26px;
        display: block;
        position: relative;
        cursor: pointer;
        transition: 0.3s;
        &::before{
            content: "";
            display: block;
            width: 26px;
            height: 26px;
            border: 1.7px solid #3F4363;
            border-radius: 8px;
            top: 0;
            left: 0;
            position: absolute;
            transition: 0.3s;
        }
        &:hover {
            &::before {
                border-color: #8F94B8CC;
                transition: 0.3s;
            }
        }
        &-input {
            visibility: hidden;
            opacity: 0;
            position: absolute;
            left: -999px;
            &:checked + .checkbox::before {
                transition: 0.3s;
                background-color: #2C2F47;
                border-color: #2C2F47;
                background-image: url('../icons/Checkmark.svg');
                background-position: center;
                background-size: auto;
                background-repeat: no-repeat;
            }
            &.error {
                background-color: black;
            }
        }
    }
    .error {
        background-color: black;
        opacity: 0.3;
    }
    .checkbox-input.error + .checkbox::before {
        border-color: red;
    }
</style>

<div class="checkbox-box">
    <input bind:this={mainCheckbox} class={`checkbox-input ${!isValid ? "error" : ''}`} type="checkbox" name="confirm-checkbox" id="checkbox" on:click={onClick}/>
    <label class="checkbox" for="checkbox"></label>
</div>