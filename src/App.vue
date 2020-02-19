<template>
    <div id="app">
        <img src="./assets/logo.png">
        <div>
            Search: <input type="text" v-model="query" placeholder="Search" />
        </div>
        <br />
        <div v-html="highlight()" contenteditable="true" @focusout="onFocusOut($event)"></div>
    </div>
</template>

<script>
    //import HelloWorld from './components/HelloWorld'

    export default {
        name: 'app',
        data() {
            return {
                query: "",
                //content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse dignissim leo massa, sed aliquet leo posuere ut. Curabitur malesuada accumsan erat, id varius eros tincidunt quis. Vivamus lobortis, odio at fermentum efficitur, risus est tincidunt nisl, eget condimentum tellus dui vitae nibh. Donec id lorem condimentum, porttitor augue in, fermentum leo. Morbi condimentum, nunc ut malesuada placerat, sem nulla condimentum purus, iaculis tristique metus diam lobortis enim. Suspendisse potenti. Quisque urna magna, porta eget erat ac, pharetra vehicula erat. Suspendisse sed nisi ex."
                content:""
            }
        },
        methods: {
            highlight() {
                //this.content = document.getElementById('area').innerHTML
                if(!this.query) {
                    return this.content;
                }
                this.content = this.content.replace(/<[^>]*>/g,'');
                return this.content.replace(new RegExp(this.query, "gi"), match => {
                    return '<span class="highlightText">' + match + '</span>';
                });
            },
            onFocusOut: function(e) {
            var elements = document.getElementsByClassName('highlightText');
  
            while(elements.length > 0){
                elements[0].classList.remove('highlightText');
            }
            this.content = e.target.innerHTML
            }
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
    .highlightText {
        background: yellow;
    }
</style>