<template>
    <div class="addItem">
        <input type="text" class="input" placeholder="Add Todo" v-model="item.name"> <!-- v-model: digunakan untuk pengambilan nama input -->
        <button class="addButton" @click="addItem()">
            <font-awesome-icon icon="plus" class="plus" /> <!-- Pemanggilan nama icon menggunakan font-awesome-icon -->
        </button>
    </div>
</template>

<script>
    export default {
        data: function () {
            return {
                item: {
                    name: "" // penamaan parameter untuk v-model
                }
            }
        },
        methods: {
            addItem() { // function click button untuk mengirim data
                if (this.item.name !== '') { // check apakah null atau tidak
                    axios.post('api/todo/store', { // function untuk memanggil api
                        todo: this.item.name // parameter yg dikirim ke body
                    }).then(response => {
                        if (response.status >= 200 & response.status < 300) { // check status response from back end
                            this.item.name = null // jadikan null input tadi
                        }
                    })
                }
            }
        }
    }

</script>

<style>
    .addItem {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 25px;
    }

    .input {
        border-style: solid;
        border-color: blue;
        border-bottom-left-radius: 4px;
        border-top-left-radius: 4px;
        border-width: 1px;
        outline: none;
        padding: 5px;
        height: 30px;
        width: 100%;
    }

    .addButton {
        height: 42px;
        width: 42px;
        border-style: solid;
        border-color: blue;
        border-bottom-right-radius: 4px;
        border-top-right-radius: 4px;
        border-width: 1px;
        background-color: white;
    }

    .plus {
        font-size: 20px;
        color: blue;
    }

</style>
