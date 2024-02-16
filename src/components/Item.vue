<template>
    <div class="card">
        <div class="card-content">
            <p>{{ cardText }}</p>
        </div>
        <div class="card-footer">
            <img :src="logoSrc" alt="Logo" class="logo">
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
        logoSrc: {
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
.card {
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 20px;
    margin: 20px;
    width: 300px;
}

.card-content {
    margin-bottom: 15px;
}

.card-footer {
    display: flex;
    align-items: center;
}

.logo {
    width: 30px;
    height: 30px;
    margin-right: 10px;
}
</style>
  