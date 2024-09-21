<script>
    import { onMount } from 'svelte';

    export let id = '';
    export let name = '';
    export let type = 'text';
    export let inputCaption = '';
    export let inputIsRequired = false;
    export let registerInput;

    let mainInput;
    let errorMessage = '';
    let isValid = true;

    onMount(() => {
        if (registerInput) {
            registerInput({ 
                element: mainInput, 
                checkValidity: checkValidity 
            });
        }
    });

    function checkValidity() {
        isValid = true;
        errorMessage = '';

        if (inputIsRequired && !mainInput.value.trim()) {
            isValid = false;
            errorMessage = 'This field is required.';
        } else {
            switch (type) {
                case 'email':
                    if (!/\S+@\S+\.\S+/.test(mainInput.value)) {
                        isValid = false;
                        errorMessage = 'Enter the correct email address.';
                    }
                    break;
                case 'tel':
                    if (!/^\d{10}$/.test(mainInput.value)) {
                        isValid = false;
                        errorMessage = 'Enter the correct phone number.';
                    }
                    break;
            }
        }

        return isValid;
    }

    function onClick(event) {
        if (event.target.classList.contains('error')) {
            event.target.classList.remove('error');
            isValid = true;
            errorMessage = ''; // Сбросить сообщение об ошибке
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
    .form {
        &-label {
            width: 100%;
            margin-bottom: 33px;
            transition: 0.3s;
            position: relative;
            &:hover {
                .form-input-caption {
                    color: #8F94B8;
                    transition: 0.3s;
                }
                .form-input {
                    border-color: #8F94B8;
                    transition: 0.3s;
                }
            }
            &:focus-within .form-input-caption {
                color: white;
            }
        }
        &-input {
            width: 100%;
            color: white;
            font-size: 18px;
            line-height: 21.6px;
            background: transparent;
            border: none;
            border-bottom: 1px solid #3F4363;
            transition: 0.3s;
            &:focus {
                outline: none;
                border-color: white !important;
                .form-input-caption {
                    color: white;
                }
            }
            &-caption {
                font-size: 15px;
                font-weight: 300;
                color: #797EA3;
                line-height: 18px;
                margin-bottom: 10px;
                transition: 0.3s;
            }
        }
    }
    
    .error {
        border-bottom: 1px solid red;
        &-text {
            position: absolute;
            color: red;
            font-size: 10px;
            margin-top: 5px;
            bottom: -16px;
            left: 0;
        }
    }
</style>
  
<label for={id} class={`form-label`}>
    <p style={!isValid ? 'color: red;' : ''} class={`form-input-caption`}>{inputCaption}{inputIsRequired ? '*' : ''}</p>
    <input 
        on:click={onClick}
        bind:this={mainInput} 
        type={type} 
        name={name} 
        id={id} 
        class={`form-input ${inputIsRequired ? 'required' : ''}`} 
        on:input={checkValidity}
    />
    <span class="error-text">{errorMessage}</span>
</label>