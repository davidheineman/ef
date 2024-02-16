<template>
    <div class="card">
        <div class="card-content">
            <p class="card-text">{{ cardText }}</p>
        </div>
        <div class="card-footer">
            <i class="fa-brands fa-twitter"></i>
            <p>{{ name }}</p>
        </div>
    </div>
</template>
  
<script>
export default {
    name: 'CardWithLogo',
    props: {
        cardText: {
            type: String,
            required: true
        },
        logo: {
            type: String,
            required: true
        },
        name: {
            type: String,
            required: true
        }
    }
};
</script>
  
<style scoped>
.card-text {
    padding: 16px
}

.card {
    border: 1px solid #ccc;
    border-radius: 5px;
    /* padding: 20px; */
    margin: 20px;
    width: 300px;
}

.card-content {
    /* margin-bottom: 15px; */
}

.card-footer {
    display: flex;
    align-items:end;
}

.logo {
    width: 30px;
    height: 30px;
    margin-right: 10px;
}
</style>
  