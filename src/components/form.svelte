<script>
    import Input from '../components/input.svelte';
    import Textarea from '../components/textarea.svelte';
    import Button from '../components/button.svelte';
    import Notification from '../components/notification.svelte';
    import Checkbox from '../components/checkbox.svelte';
    let requiredInputs = [];
    let showNotification = false;

    function validateForm(event) {
        event.preventDefault();
        let invalidInputs = [];

        requiredInputs.forEach(input => {
            const isValid = input.checkValidity();
            if (!isValid) {
                invalidInputs.push(input);
            }
        });

        if (invalidInputs.length > 0) {
            invalidInputs.forEach(input => {
                input.element.classList.add('error');
            });
        } else {
            requiredInputs.forEach(input => {
                input.element.classList.remove('error');
                input.element.value = '';
                showNotification = true;
                setTimeout(() => {
                    showNotification = false;
                }, 5000);
            });
        }
    }

    function registerInput(input) {
        if (input) {
            requiredInputs.push(input);
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

    .main {
        &-title {
            text-align: center;
            color: white;
            font-weight: 500;
            font-size: 55px;
        }
        &-form {
            width: 390px;
            border-radius: 27px;
            background-color: #171929;
            padding: 40px 45px 40px 45px;
            box-shadow: 0px 0px 50px 0px #000000B2;
        }
    }

    .form {
        &-container {
            display: flex;
            justify-content: center;
        }
        &-header {
            text-align: center;
            padding: 0 20px 10px;
            &-text {
                color: white;
                font-size: 18px;
                font-weight: 400;
                line-height: 21.6px;
                margin-bottom: 11px;
            }
            &-hint {
                color: #797EA3;
                font-size: 15px;
                font-weight: 300;
                line-height: 18px;
            }
        }
        &-body {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
    }

    .confirmation {
        color: white;
        font-weight: 300;
        font-size: 15px;
        line-height: 18px;
        margin: 26px 0 36px;
        display: flex;
        align-items: center;
        gap: 16px;
        position: relative;
        a {
            color: #797EA3;
        }
    }
</style>

{#if showNotification}
    <Notification notificationMessage="The form has been successfully submitted!"/>
{/if}
<h1 class="main-title">Hello!</h1>
<div class="form-container">
    <form method="post" class="main-form" on:submit={validateForm}>
        <div class="form-header">
            <p class="form-header-text">For business enquiries please use the form below</p>
            <p class="form-header-hint">*Required</p>
        </div>
        <div class="form-body">
            <Input registerInput={registerInput} type="text" id="name-input" name="name" inputCaption="Name" inputIsRequired={true} />
            <Input registerInput={registerInput} type="text" id="company-input" name="company" inputCaption="Company" inputIsRequired={true} />
            <Input registerInput={registerInput} type="email" id="email-input" name="email" inputCaption="E-mail" inputIsRequired={true} />
            <Input registerInput={registerInput} type="number" id="phone-input" name="phone" inputCaption="Phone" inputIsRequired={false} />
            <Input registerInput={registerInput} type="text" id="subject-input" name="subject" inputCaption="Subject" inputIsRequired={false} />
            <Textarea registerInput={registerInput} type="text" id="message-input" name="message" inputCaption="Message" inputIsRequired={true} />
            <div class="confirmation">
                <Checkbox registerInput={registerInput}/> <span>I accept <a href="https://www.youtube.com/watch?v=xvFZjo5PgG0&ab_channel=Duran">Terms and Privacy Policy</a></span>
            </div>
            <Button styles="background-color: #2C2F47;"/>
        </div>
    </form>
</div>