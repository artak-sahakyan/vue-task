<template>
  <div>

    <div>


      <div>
          <pre><code>
            {{jsonData}}
          </code></pre>
      </div>

      <select v-model="chosenColor">
        <option v-for="color in colors" :value="color" :key="'color_' + color">{{color}}</option>
      </select>

      <select v-model="chosenBackground">
        <option v-for="color in colors" :value="color" :key="'bgcolor_' + color">{{color}}</option>
      </select>

      <select v-model="chosenSize">
        <option v-for="size in sizes" :value="size+'px'" :key="'size_' + size">{{size}}</option>
      </select>

      <button type="button" @click="exportToJson">Export To Json</button>

    </div>


    <selected-text v-for="(item, index) in items"
                   :key="'item_' + index"
                   :color="item.color"
                   :font="item.font"
                   :background="item.background"
                   :text="item.text"
                   @textSelected="initTextControls(index, $event)"
    />


  </div>
</template>

<script>
  import SelectedText from './SelectedText'

  export default {
    name: 'Editor',
    components: {SelectedText},
    methods: {
      initTextControls(index, event) {
        this.chosenColor = event.color;
        this.chosenSize = event.font;
        this.chosenBackground = event.background;
        this.activeKey = index;
      },

      exportToJson() {
        this.jsonData = JSON.stringify(this.items);
        console.log(this.jsonData)
      }
    },

    watch: {
      chosenColor() {
        this.items[this.activeKey].color = this.chosenColor;
      },
      chosenBackground() {
        this.items[this.activeKey].background = this.chosenBackground;
      },
      chosenSize() {
        this.items[this.activeKey].font = this.chosenSize;
      },
    },

    data() {
      return {


        jsonData: '',
        activeKey: 0,
        chosenColor: 'white',
        chosenSize: '8px',
        chosenBackground: 'black',


        colors: [
          'black', 'white', 'green', 'yellow', 'brown', 'blue', 'orange'
        ],

        sizes: [
          8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30
        ],


        items: [
          {
            color: 'green',
            font: '18px',
            background: 'red',
            text: 'Hi'

          },
          {
            color: 'green',
            font: '18px',
            background: 'green',
            text: 'My lovely'

          },
          {
            color: 'blue',
            font: '18px',
            background: 'yellow',
            text: 'little'

          },
          {
            color: 'blue',
            font: '18px',
            background: 'yellow',
            text: 'Ponny'

          },
        ]
      }

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
