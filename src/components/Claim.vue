<template>
    <div class="claimWrapper">
        <h1 class="claim">SPACER</h1>
        <p class="subclaim">
            Begin your journey through our galaxy, and discover places you never evend heard of.
        </p>
        <p class="subclaim">
            Type anything splace-related to start.
        </p>
    </div>
</template>

<script>

export default {
    name: 'Claim',
};

</script>


<style lang="scss" scoped>
.claimWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.claim {
    font-size: 50px;
    margin: 0;
}

.subclaim {
    margin-top: 20px 0 0 0;
    font-size: 13px;
}
</style>
