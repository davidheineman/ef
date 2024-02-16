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
                <h2>Choose How to Resolve</h2>
                <p>Client Complaint</p>
                <p class="card-text" v-html="formattedText"></p>
                <p>Suggested Response</p>
                <p>{{ response }}</p>
                <button class="send">Send</button>
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
            resposnse: ''
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
                this.response = response;
            });
        },
        async getResponse() {
            try {
                const prompt = `Here is a negative customer review: "You know what's scarier than a horror movie? Wells Fargo's fees. #NightmareBank". 
                Write a polite and empathetic response that offers a solution to the customer's problem. BE CONCISE, do not exceed 250 characters Make sure you address the user's specific concerns if any are mentioned.`;

                const completion = await openai.chat.completions.create({
                    messages: [{ role: "system", content: prompt }],
                    model: "gpt-3.5-turbo",
                });

                console.log(completion)
                return completion.choices[0].message.content;
            } catch (error) {
                console.error('Error in generating solution:', error);
                return 'Sorry, there was an error processing the review.';
            }
        },
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
  width: 30%;
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
</style>
  