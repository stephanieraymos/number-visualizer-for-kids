<template>
    <div class="container">
        <div class="top-section">
            <div>
                <input type="number" v-model="number" />
                <button @click="setTheNumber">Calculate</button>
            </div>

            <!-- Choose an image to display -->
            <select
                name="image"
                id="selectedImage"
                v-model="selected"
                @change="setTheImage(selected)"
            >
                <option disabled value="">Select an object to display</option>
                <option value="cat">Cat</option>
                <option value="dog">Dog</option>
                <option value="bird">Bird</option>
                <option value="penny">Penny</option>
                <option value="nickle">Nickle</option>
                <option value="dime">Dime</option>
                <option value="quarter">Quarter</option>
                <option value="marble">Marble</option>
            </select>

            <div class="fun-fact-container">
                <h3>Fun Facts</h3>
                <p>
                    The number you entered is
                    <span v-if="number % 2 === 0">even</span>
                    <span v-else>odd</span>
                </p>
                <p v-if="imageToDisplay.name === 'Dime'">
                    A dime is worth 10 cents
                </p>
                <p v-else-if="imageToDisplay.name === 'Nickle'">
                    A nickle is worth 5 cents
                </p>
                <p v-else-if="imageToDisplay.name === 'Penny'">
                    A penny is worth 1 cent
                </p>
                <p v-else-if="imageToDisplay.name === 'Quarter'">
                    A quarter is worth 25 cents
                </p>
                <p v-else-if="imageToDisplay.name === 'Marble'">
                    A marble is a toy
                </p>
                <p v-else-if="imageToDisplay.name === 'dog'">A dog is a pet</p>
                <p v-if="imageToDisplay.name === 'cat'">
                    Cats are majestic, magical creatures
                </p>
                <p v-if="imageToDisplay.name === 'cat' && number > 100">
                    Wow! More than 100 cats!? That's a lot of love!
                </p>

                <!-- <p v-else-if="imageToDisplay.name === 'cat'">
                Cats are magestic, magical creatures
                {{
                    number > 100
                        ? "Wow, more than 100 cats! That's a lot of love!"
                        : ''
                }}
            </p> -->
                <p v-else-if="imageToDisplay.name === 'bird'">
                    A bird is a pet
                </p>
            </div>
        </div>
        <div v-if="number <= 1000">
            <div class="result-container">
                <span v-for="singleItem in number" :key="singleItem">
                    <img
                        :src="imageToDisplay.src"
                        :name="imageToDisplay.alt"
                        :alt="imageToDisplay.alt"
                        :class="getObjectClass(imageToDisplay)"
                    />
                </span>
            </div>
        </div>
        <div v-else>
            <h2 style="color: white">
                Number is too large to display, try a number less than 1000.
            </h2>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const number = ref(10);
const selected = ref('cat'); // Default selected option
const imageToDisplay = ref({
    src: require('../assets/cat.png'),
    alt: 'Cat',
    size: 'large',
    name: 'cat',
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
        case 'nickle':
            size = 'medium';
            break;
        case 'quarter':
        case 'cat':
        case 'dog':
        case 'bird':
            size = 'large';
            break;
        default:
            size = 'medium';
    }

    imageToDisplay.value = {
        src: require(`../assets/${selectedImage}.png`),
        alt: selectedImage.charAt(0).toUpperCase() + selectedImage.slice(1),
        size: size,
        name: selectedImage.charAt(0).toUpperCase() + selectedImage.slice(1),
    };
};

const getObjectClass = object => {
    return `singleItem-${object.size}`;
};
</script>

<style scoped>
.container {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    padding: 2rem;
}
.fun-fact-container {
    border: 1px solid #ccc;
    border-radius: 5px;
    background: var(--color-purple);
    color: white;
    flex-basis: 50%;
}
.top-section {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.result-container {
    margin-top: 20px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    align-content: center;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background: var(--light-color-3);
    min-height: 80vh;
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
