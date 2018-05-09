<template>
    <div>
        <header>
            <div class="info-bar text-center">
                Get $50 Off + $15 Credit*
            </div>
            <div class="container">
                <div class="header-container row">
                <div class="col no-padding text-left">
                    <img src="/shipt-logo.png" class="main-logo" alt="Shipt-logo">
                </div>
                <div class="col no-padding text-right">
                    <button>
                    SIGN UP
                    </button>
                </div>
                </div>
            </div>
        </header>
    </div>
</template>

<style scoped>
header {
    box-shadow: 0px 2px 10px 0px rgba(0, 0, 0, .1);
    background-color: #FFF;
    margin-bottom: 16px;
}

.main-logo {
    width: 128px;
    height: 48px;
}

.header-container {
    padding: 18px 0px;
}

.info-bar {
    background-color: #414042;
    font-family: 'Scandia-Bold';
    text-transform: uppercase;
    letter-spacing: 1.5px;
    font-size: 11px;
    transition: background-color .2s ease;
    padding: 4px 0px;
    color: #FFF;
    width: 100%;
}

.info-bar:hover {
    background-color: #71B045
}

/* / Media Queries /  */

@media only screen and (max-width: 600px) {
    header {
        box-shadow: none;
        margin-bottom: 0px;
    }


}

@media only screen and (min-width: 600px) {
    .no-padding {
        padding: 0px;
    }
}
</style>