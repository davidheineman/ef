<template>
    <div class="card" @click="toggleModal">
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

        <div v-if="showModal" class="modal">
            <div class="modal-content">
                <h2>Resolution</h2>
                <hr>
                <h3>Client Complaint</h3>
                <div class="centerthis" style="margin-top:8px">
                    <div class="card border-dark mb-3" style="max-width: 18rem;">
                        <div class="card-body text-dark">
                            <p class="card-text">
                            <p class="card-text" v-html="formattedText"></p>
                            </p>
                        </div>
                    </div>
                </div>
                <h3>Suggested Responses</h3>
                <div class="response">
                    <p>{{ response1 }}</p>
                    <button type="button" class="btn btn-primary">Send</button>
                </div>
                <div class="response">
                    <p>{{ response2 }}</p>
                    <button type="button" class="btn btn-primary">Send</button>
                </div>

                <!-- <div class="row">
    <div class="col-md-auto">
        <button type="button" class="btn btn-primary">Send</button>
    </div>
    <div class="col-md-auto">
        <button type="button" class="btn btn-warning">Tag for later</button>
    </div>
</div> -->
            </div>
        </div>
    </div>
</template>
  
<script>
// import Modal from './Modal.vue';
import OpenAI from "openai";
import data from '../../env.json';


const apiKey = data.VUE_APP_OPENAI_API_KEY;

const openai = new OpenAI({
    apiKey: apiKey,
    dangerouslyAllowBrowser: true
});

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
            showModal: false,
            response1: 'Generating response 1...',
            response2: 'Generating response 2...'
        };
    },
    computed: {
        formattedText() {
            let rawHTML = this.cardText.map(([word, label]) => `<span class="${label}">${word}</span>`).join(' ');
            return rawHTML;
        }
    },
    methods: {
        toggleModal() {
            this.showModal = !this.showModal;
            this.getResponse().then(response => {
                this.response1 = response[0].message.content;
                this.response2 = response[1].message.content;
            });
        },
        async getResponse() {
            try {
                const prompt = `Here is a negative customer review: "You know what's scarier than a horror movie? Wells Fargo's fees. #NightmareBank". 
                Write a polite and empathetic response that offers a solution to the customer's problem. BE CONCISE, do not exceed 250 characters Make sure you address the user's specific concerns if any are mentioned.`;

                const completion = await openai.chat.completions.create({
                    messages: [{ role: "system", content: prompt }],
                    model: "gpt-3.5-turbo",
                    n: 2,
                });

                console.log(completion)
                return completion.choices;
            } catch (error) {
                console.error('Error in generating solution:', error);
                return 'Sorry, there was an error processing the review.';
            }
        },
    }
};
</script>
  
<style scoped>
.response {
    padding: 0 16px 0 0;
}

.response p {
    padding-right: 16px
}

.response button {
    height: 50px !important;
}

    .centerthis {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%; /* Adjust as needed */
    }

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
    justify-content: flex-end;
    /* Align items to the right */
}

.card-footer p {
    margin-bottom: 8px;
}

.logo {
    width: 30px;
    height: 30px;
    margin-right: 10px;
}

.modal {
    display: block;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 50%;
}

.close {
    color: #aaa;
    display: flex;
    font-size: 28px;
    font-weight: bold;
}

.close:hover,
.close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
}

.response {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
}

.send {
    width: 80px;
    height: 30px;
}
</style>
  