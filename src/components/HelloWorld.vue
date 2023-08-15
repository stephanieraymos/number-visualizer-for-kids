<template>
    <div class="number-container">
        <input type="number" v-model="number" />
        <button @click="setTheNumber">Calculate</button>
        <p>Result: {{ result }}</p>
        <div class="result-container">
            <!-- <span v-for="number " :key="number">
                <span v-for="image in page" :key="image.alt">
                    <img :src="image.src" :alt="image.alt" class="item-shown" />
                </span>
            </span> -->
            <span v-for="singleItem in number" :key="singleItem">
                <img
                    :src="imageToDisplay.src"
                    :alt="imageToDisplay.alt"
                    :class="getObjectClass(imageToDisplay)"
                />
            </span>
        </div>
    </div>
    <div>
        <!-- Choose an image to display -->
        <select
            name="image"
            id="selectedImage"
            v-model="selected"
            @change="setTheImage(selected)"
        >
            <option disabled value="">Please select one</option>
            <option value="cat">Cat</option>
            <option value="dog">Dog</option>
            <option value="bird">Bird</option>
            <option value="penny">Penny</option>
            <option value="nickle">Nickle</option>
            <option value="dime">Dime</option>
            <option value="quarter">Quarter</option>
            <option value="marble">Marble</option>
        </select>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const number = ref(10);
const selected = ref('cat'); // Default selected option
const imageToDisplay = ref({
    src: require('../assets/cat.png'),
    alt: 'Cat',
    size: 'small',
});
// why is the src above wrong
// the src above is wrong because it is not in the public folder
// the correct src is '@/assets/cat'
// Function to handle the button click
const setTheNumber = () => {
    number.value = number;
};

const setTheImage = selectedImage => {
    let size;
    switch (selectedImage) {
        case 'penny':
        case 'dime':
        case 'marble':
            size = 'small';
            break;
        case 'cat':
        case 'dog':
        case 'bird':
        case 'nickle':
            size = 'medium';
            break;
        case 'quarter':
            size = 'large';
            break;
        default:
            size = 'medium';
    }

    imageToDisplay.value = {
        src: require(`../assets/${selectedImage}.png`),
        alt: selectedImage.charAt(0).toUpperCase() + selectedImage.slice(1),
        size: size,
    };
    console.log('image.src was set to: ', imageToDisplay.value.src);
};

const getObjectClass = object => {
    return `singleItem-${object.size}`;
};
</script>

<style scoped>
.number-container {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    padding: 2rem;
    background: #09001e;
}
.result-container {
    margin-top: 20px;
    display: flex;
    flex-wrap: wrap;
}
.item-shown {
    height: 50px;
    margin: 1px;
}
.singleItem-small {
    width: 40px;
}

.singleItem-medium {
    width: 60px;
}

.singleItem-large {
    width: 80px;
}
</style>
