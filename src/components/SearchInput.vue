<template>
    <div class="searchWrapper">
        <input @input="handleInput" id="search" name="search" v-model="searchValue" />
    </div>

</template>

<script>

export default {
    name: 'SearchInput',
};

</script>


<style lang="scss" scoped>
.searchWrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 300px;

    input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid black;
        background: none;
    }
}

</style>
