<template>
  <input type="text" style="background: transparent; border: none"
         v-model="inputText"
         v-if="showInput"
         ref="textForm"
         @blur="closeInput"
         @keyup.enter="addBreak"/>
  <span v-else :style="style" @click="openInput" v-html="inputText + printBreaks"></span>
</template>

<script>
  export default {
    name: 'SelectedText',
    props: {
      text: String,
      background: String,
      font: String,
      color: String,
    },
    data() {
      return {
        showInput: false,
        inputText: this.text,
        breaks: 0
      }
    },
    methods: {
      addBreak() {
        this.breaks++;
        this.showInput = false
      },
      openInput() {
        this.showInput = true;
        setTimeout(() => {
          this.$refs.textForm.focus();
        }, 10);
        this.$emit('textSelected', this.$options.propsData)
      },
      closeInput() {
        this.showInput = false
      }
    },

    computed: {

      printBreaks() {
        let breaksHtml = '';
        for (let i = 0; i < this.breaks; i++) {
          breaksHtml += '<br />';
        }
        return breaksHtml;
      },

      style() {
        return {
          'background-color': this.background,
          'padding-left': '3px',
          'padding-right': '3px',
          'border-radius': '4px',
          'font-size': this.font,
          'color': this.color
        }
      }
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  span {
    margin-left: 5px;
    margin-right: 5px;
  }
</style>
