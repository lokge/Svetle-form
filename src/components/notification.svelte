<script>
    export let notificationMessage = 'The form has been successfully submitted!';
    export let timer = '500ms';
    export let notification;
</script>

<style lang="scss">
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-weight: 400;
        font-family: 'Roboto', sans-serif;
    }
    
    .notification {
        position: fixed;
        left: 50%;
        transform: translateX(-50%);
        &-content {
            width: 210px;
            height: 50px;
            border-top-left-radius: 9px;
            border-top-right-radius: 9px;
            border-bottom-left-radius: 5px;
            border-bottom-right-radius: 5px;
            text-align: center;
            color: white;
            padding: 5px 10px;
            -webkit-box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.75);
            -moz-box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.75);
            box-shadow: 0px 0px 10px 4px rgba(0,0,0,0.75);
            position: relative;
        }
        &-load {
            position: absolute;
            left: 0;
            bottom: 0;
            background-color: #3acb7d;
            height: 5px;
            width: 100%;
            border-bottom-left-radius: 9px;
            border-bottom-right-radius: 9px;
            &-bar {
                display: block;
                width: 100%;
                height: 100%;
                background: #4caf50;
                animation: loadingAnimation 5000ms linear forwards;
                border-bottom-left-radius: 9px;
            }
        }
    }
    .success {
        background: linear-gradient(90deg,rgba(0,128,82,.91) .01%,#1a1c20);
    }

    @keyframes loadingAnimation {
        from {
            width: 100%;
        }
        to {
            width: 0%;
        }
    }
</style>

<div bind:this={notification} class="notification">
    <div class="notification-content success">
        <p>{notificationMessage}</p>
        <div class="notification-load"><span class="notification-load-bar"></span></div>
    </div>
</div>