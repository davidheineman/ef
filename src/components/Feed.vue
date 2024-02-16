<template>
    <div class="feed">
        <div class="container">
            <div class="row">
                <div class="col-lg-8 offset-lg-2">
                    <div class="card">
                        <div class="card-header">
                            Feed
                        </div>
                        <div class="card-body">
                            <div class="scrollable-feed">
                                <div v-for="(item, index) in items" :key="index" class="feed-item">
                                    {{ item }}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <Item cardText="This is the text in the card." logoSrc="/path/to/logo.png" name="Company Name" />
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
                "Item 1",
                "Item 2",
                "Item 3",
                // Add more items as needed
            ]
        };
    }
};
</script>
  
<style scoped>
.scrollable-feed {
    max-height: 400px;
    /* Adjust height as needed */
    overflow-y: auto;
}

.feed-item {
    padding: 10px;
    border-bottom: 1px solid #ccc;
}

/* Optional styling for better appearance */
.card {
    margin-top: 20px;
}

.card-header {
    background-color: #f8f9fa;
    border-bottom: 1px solid #dee2e6;
    font-weight: bold;
}

.card-body {
    padding: 0;
}
</style>
  