<template>
    <div class="feed">
        <div class="container">
            <div class="row">
                <div class="col-lg-6">
                    <div class="card">
                        <div class="card-header">
                            Feed
                        </div>
                        <div class="card-body">
                            <!-- <Item :cardText="devtext" logo="fa-brands fa-twitter" name="Twitter" /> -->


                            <div class="scrollable-feed">
                                <div v-for="(item, index) in displayItems" :key="index" class="feed-item">
                                    <Item :cardText="item" logo="fa-brands fa-twitter" name="Twitter" />
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import Item from './Item.vue';

export default {
    components: {
        Item
    },
    data() {
        return {
            items: [
                [["Wells", "BRAND"], ["Fargo", "BRAND"], [":", "O"], ["Making", "FRUST"], ["bad", "FRUST"], ["decisions", "FRUST"], ["since", "O"], ["forever", "O"], [".", "O"], ["#", "SERV"], ["WorstBankEver", "SERV"]],
                [["Thanks", "O"], [",", "O"], ["Wells", "BRAND"], ["Fargo", "BRAND"], [",", "O"], ["for", "O"], ["charging", "O"], ["me", "O"], ["fees", "PROD"], ["just", "O"], ["for", "O"], ["existing", "O"], [".", "O"], ["#", "O"], ["NotCool", "FRUST"]],
                [["Wells", "BRAND"], ["Fargo", "BRAND"], ["customer", "SERV"], ["service", "SERV"], [":", "O"], ["Where", "O"], ["dreams", "O"], ["go", "O"], ["to", "O"], ["die", "O"], [".", "O"], ["#", "O"], ["CustomerServiceFail", "FRUST"]],
                [["Guess", "O"], ["who", "O"], ["messed", "O"], ["up", "O"], ["my", "O"], ["account", "O"], ["again", "O"], ["?", "O"], ["Yep", "O"], [",", "O"], ["you", "O"], ["guessed", "O"], ["it", "O"], [",", "O"], ["Wells", "BRAND"], ["Fargo", "BRAND"], [".", "O"], ["#", "O"], ["NeverAgain", "FRUST"]],
                [["Wells", "BRAND"], ["Fargo", "BRAND"], [":", "O"], ["where", "FRUST"], ["incompetence", "FRUST"], ["meets", "O"], ["greed", "FRUST"], [".", "O"], ["#", "SERV"], ["WorstBankEver", "SERV"]],
                [["Trying", "O"], ["to", "O"], ["reach", "O"], ["Wells", "BRAND"], ["Fargo", "BRAND"], ["support", "SERV"], ["is", "O"], ["like", "O"], ["shouting", "O"], ["into", "O"], ["the", "O"], ["void", "O"], [".", "O"], ["#", "O"], ["NoHelp", "FRUST"]],
                [["Wells", "BRAND"], ["Fargo", "BRAND"], ["'s", "O"], ["idea", "O"], ["of", "O"], ["'", "O"], ["convenience", "PROD"], ["'", "O"], ["is", "O"], ["robbing", "FRUST"], ["you", "O"], ["blind", "O"], [".", "O"], ["#", "O"], ["Ripoff", "FRUST"]]
            ],

            // items: [
            //     "Wells Fargo: Making bad decisions since forever. #WorstBankEver",
            //     "Thanks, Wells Fargo, for charging me fees just for existing. #NotCool",
            //     "Wells Fargo customer service: Where dreams go to die. #CustomerServiceFail",
            //     "Guess who messed up my account again? Yep, you guessed it, Wells Fargo. #NeverAgain",
            //     "Wells Fargo: where incompetence meets greed. #WorstBankEver",
            //     "Trying to reach Wells Fargo support is like shouting into the void. #NoHelp",
            //     "Wells Fargo's idea of 'convenience' is robbing you blind. #Ripoff",
            //     "Hey Wells Fargo, ever heard of 'ethical banking'? Didn't think so. #Shameful",
            //     "Wells Fargo: You'll never find a more wretched hive of scum and villainy. #Avoid",
            //     "Wells Fargo: Where fees multiply like rabbits. #MoneyPit",
            //     "If you're looking for disappointment, look no further than Wells Fargo. #Fail",
            //     "Wells Fargo's motto: 'Let's make banking as frustrating as possible.' #MissionAccomplished",
            //     "I'd rather wrestle a bear than deal with Wells Fargo again. #BankingNightmare",
            //     "Wells Fargo: Where customer satisfaction goes to die. #NoThanks",
            //     "Wells Fargo: The epitome of corporate greed. #MoneyHungry",
            //     "I'd rather trust a toddler with my finances than Wells Fargo. #NoFaith",
            //     "Shoutout to Wells Fargo for consistently ruining my day. #ThanksForNothing",
            //     "Wells Fargo: Where your money disappears without a trace. #Sketchy",
            //     "Wells Fargo's idea of 'security' is a joke. #Unsafe",
            //     "You know what's scarier than a horror movie? Wells Fargo's fees. #NightmareBank",
            // ],
            currentItemIndex: 1,
            displayItems: []
        };
    },
    created() {
        this.startFeed();
    },
    methods: {
        startFeed() {
            setInterval(() => {
                if (this.currentItemIndex < this.items.length) {
                    // Add the new item to the beginning of the displayItems array
                    this.displayItems.unshift(this.items[this.currentItemIndex]);
                    this.currentItemIndex++;
                } else {
                    clearInterval(this.interval);
                }
            }, 2000);
        }
    }
};
</script>
  
<style scoped>
.scrollable-feed {
    max-height: 800px;
    overflow-y: auto;
}

.feed-item {
    padding: 10px 10px 10px 10px;
    /* border-bottom: 1px solid #ccc; */
}

/* Optional styling for better appearance */
.card {
    margin-top: 20px;
    width: 500px
}

.card-header {
    background-color: #f8f9fa;
    border-bottom: 1px solid #dee2e6;
    font-weight: bold;
}

.card-body {
    padding: 16px 0 16px 0;
}
</style>
  