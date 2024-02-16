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
                            <div class="scrollable-feed">
                                <div v-for="(item, index) in items" :key="index" class="feed-item">
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
        Item,
        Item
    },
    data() {
        return {
            items: [
                "Wells Fargo: Making bad decisions since forever. #WorstBankEver",
                "Thanks, Wells Fargo, for charging me fees just for existing. #NotCool",
                "Wells Fargo customer service: Where dreams go to die. #CustomerServiceFail",
                "Guess who messed up my account again? Yep, you guessed it, Wells Fargo. #NeverAgain",
                "Wells Fargo: where incompetence meets greed. #WorstBankEver",
                "Trying to reach Wells Fargo support is like shouting into the void. #NoHelp",
                "Wells Fargo's idea of 'convenience' is robbing you blind. #Ripoff",
                "Hey Wells Fargo, ever heard of 'ethical banking'? Didn't think so. #Shameful",
                "Wells Fargo: You'll never find a more wretched hive of scum and villainy. #Avoid",
                "Wells Fargo: Where fees multiply like rabbits. #MoneyPit",
                "If you're looking for disappointment, look no further than Wells Fargo. #Fail",
                "Wells Fargo's motto: 'Let's make banking as frustrating as possible.' #MissionAccomplished",
                "I'd rather wrestle a bear than deal with Wells Fargo again. #BankingNightmare",
                "Wells Fargo: Where customer satisfaction goes to die. #NoThanks",
                "Wells Fargo: The epitome of corporate greed. #MoneyHungry",
                "I'd rather trust a toddler with my finances than Wells Fargo. #NoFaith",
                "Shoutout to Wells Fargo for consistently ruining my day. #ThanksForNothing",
                "Wells Fargo: Where your money disappears without a trace. #Sketchy",
                "Wells Fargo's idea of 'security' is a joke. #Unsafe",
                "You know what's scarier than a horror movie? Wells Fargo's fees. #NightmareBank",
            ]
        };
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
  