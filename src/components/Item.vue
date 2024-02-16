<template>
    <div class="card" @click="showModal = true">
        <div class="card-content">
            <!-- <p class="card-text">{{ cardText }}</p> -->
            <p class="card-text" v-html="formattedText"></p>
        </div>
        <div class="card-footer">
            <i class="fa-brands fa-twitter"></i>
            <p style="margin-bottom: 0">
                <p style="text-align: right; margin-bottom: 0;">{{ name }}</p>
                <p style="text-align: right; margin-bottom: 0;">@username</p>
            </p>
        </div>

        <div class="modal-overlay" v-if="showModal">
            <div class="modal">
                <span class="close" @click="showModal = false">&times;</span>
                <div class="modal-content">
                    <h2>Modal Title</h2>
                    <p>This is the content of the modal.</p>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
// import Modal from './Modal.vue';

export default {
    name: 'CardWithLogo',
    props: {
        cardText: {
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
    },
    data() {
        return {
            showModal: false // Initially modal is hidden
        };
    },
    computed: {
        formattedText() {

            let rawHTML = this.cardText.map(([word, label]) => `<span class="${label}">${word}</span>`).join(' ');
            return rawHTML;
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
    margin: 0 20px 0 20px;
    margin-top: 0 !important;
    width: 90% !important;
}

.card-content {
    /* margin-bottom: 15px; */
}

.card-footer {
    display: flex;
    align-items: end;
    justify-content: flex-end; /* Align items to the right */
}

.card-footer p {
    margin-bottom: 8px;
}

.logo {
    width: 30px;
    height: 30px;
    margin-right: 10px;
}</style>
  