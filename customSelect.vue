<template>
    <div class="select_body">
        <select class="input" :name="name" v-model="selected">
            <option v-for="(value, index) in values" :value="index" :key="index">{{value}}</option>
        </select>
        <div class="select" @click="changeActive"  :class="{active: isActive}">  <!-- Button for open options -->
            <p>{{select}}</p> <!-- The selected value will be written here -->
            <p>{{arrow}}</p>
        </div>
        <div class="options" :class="{active: isActive}"> <!-- Options -->
            <p class="option" :class="'option' + index" v-for="(value, index) in values" :key="index" @click="changeSelect(value, index)">{{value}}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        values: {
            type: Array,
            required: true,
        },
        placeholder: {
            type: String,
            default: ''
        },
        arrow: {
            type: String,
            default: '▼'
        },
        name: {
            type: String,
            default: '',
        }
    },
    data() {
        return {
            select: this.values[0],
            isActive: false,
            selected: this.values.findIndex(i => i == this.values[0]),
        }
    },
    methods: {
        changeActive(){
            this.isActive = !this.isActive;
        },
        changeSelect(value, index){
            this.select = value;
            this.isActive = false;

            this.selected = index;
        }
    },
    mounted(){
        /* Check not empty prop placeholder */
        this.placeholder != '' ? this.select=this.placeholder : false;

        /* Check which option now select */
        this.select != this.values[this.selected] ? this.select=this.values[this.selected] : false;
    },
}
</script>

<style>
    *{
        padding: 0;
        margin: 0;
    }
    
    /* Select body */
    .select_body .select{
        display: flex;
        justify-content: space-between;
        width: 150px;
        border: 1px solid black;
        padding: 10px 15px;
        cursor: pointer;
        border-radius: 10px;
        font-size: 1.458vw;
        transition: 0.3s ease all;
    }

    .select_body .select:hover{
        border-color: grey;
        box-shadow: 0 0 20px grey;
    }

    .select_body .select p:last-of-type{
        transition: 0.2s ease all;
    }

    /* Text in header select */
    .select_body .select p:first-of-type{
        color: black;
    }

    /* Arrow */
    .select_body .select:hover p:last-of-type{
        color: black;
    }

    /* .select when this active */
    .select_body .select.active{
        border-bottom: 1px solid grey;
        border-radius: 10px 10px 0 0;
    }

    /* rotate arrow when select active */
    .select.active p:last-of-type{
        transform: rotate(0.5turn);
    }

    /* clear :hover when selecr active */
    .select.active:hover{
        border-color: black;
        box-shadow: none;
    }

    .select.active:hover p:last-of-type{
        color: black;
    }

    /* options */

    .select_body .options{
        display: none;
        position: absolute;
    }

    /* options when select active */
    .select_body .options.active{
        display: flex;
        flex-direction: column;
    }

    /* One option */
    .option{
        width: 150px;
        border-left: 1px solid black;
        border-right: 1px solid black;
        padding: 10px 15px;
        cursor: pointer;
        font-size: 1.458vw;
        transition: 0.3s ease all;
        background-color: white;
    }

    .option:hover{
        background: grey;
    }

    /* style border of last option */
    .select_body .option:last-of-type{
        border-bottom: 1px solid black;
        border-radius: 0 0 10px 10px;
    }
</style>