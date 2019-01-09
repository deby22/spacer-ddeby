<template>
    <input 
    id="search"
    name="search"
    :class="{ dark }"
    :value="value"
    @input="handleChange"
    />
</template>

<script>

export default {
    name: 'SearchInput',
    props: {
        value: {
            type:String,
            required: true,
        },
        dark: {
            type: Boolean,
            default: false,
        },
    },
    methods: {
        handleChange(e) {
            this.$emit('input', e.target.value);
        },
    },
};

</script>


<style lang="scss" scoped>
input {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 275px;

        color: white;
        text-align: center;
        font-size: 18px;
        font-weight: 300;
        height: 30px;
        border: 0;
        border-bottom: 1px solid white;
        background: none;
    }

    input:focus{
        outline: none;
        box-shadow: 0 10px 20px -8px rgba(255, 255, 255, .2);
    }

    .dark {
        color: #1e3d4a;
        border-bottom-color: #1e3d4a;
    }

    .dark:focus {
        box-shadow: 0 10px 20 px -8px rgba(#1e3d4a, .2);
    }

</style>
