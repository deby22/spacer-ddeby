<template>
    <div id="app">
        <div id="nav">
            <router-link to="/">Spacer</router-link>
        </div>
        <router-view/>
    </div>
</template>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');
*{
    box-sizing: border-box;
}

body {
    font-family: 'Montserrat', sans-serif;
}
</style>
