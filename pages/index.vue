<template>

    <section class="container">
        <item-description></item-description>
        <h1 class="title">
            {{message | capitalize}}
        </h1>
        <button @click="changeMessage" class="button">Change Message</button>
        <hr>
        <section>
            <h2>Mouse event</h2>
            <div>{{counter}}</div>
            <template v-if="counter > 5">
                <div>Show if the counter is greater than five</div>
            </template>
            <div v-else>Show the counter is smaller than five</div>
            <button @click="dec" v-show="counter > 0">-</button>
            <button @click="inc" v-show="counter < 5">+</button>
            <div @mouseover="inc">Mouse over here to change counter</div>
        </section>
        <section>
            <h2>Keyboard events</h2>
            <form @submit.prevent="submit">
                <input type="text"
                       v-model="firstName"
                       @keyup.enter="submit"
                       @keyup.alt.ctrl.shift.down="keyeventHandler"/>
                <button v-bind:disabled="buttonDisabled">{{buttonText}}</button>
            </form>
            <div>
                {{key}}
            </div>
        </section>
    </section>
</template>

<style scoped>
.title
{
  margin: 50px 0;
}

</style>

<script>

  import ItemDescription from '../components/item-description';

  export default {
    data() {
      return {
        message: 'this is my vue!',
        counter: 0,
        key: "",
        firstName: "",
        buttonText: "Add"
      }
    },

      computed: {
        buttonDisabled: function() {
          return this.firstName == "";
        }
      },
      watch: {
        firstName: function(){
          this.buttonText = this.firstName !== "" ? "Add " + this.firstName : "Add Dinosaur";
        }
      },

    components: {
        ItemDescription
    },

    filters: {
        capitalize(value) {
            return value.charAt(0).toUpperCase() + value.slice(1).toLowerCase();
        }
    },

    methods: {
      changeMessage() {
        this.message = "Updated message here!"
      },

      inc() {
        this.counter += 1;
      },

      dec() {
        this.counter -= 1;
      },

      keyeventHandler() {
        this.key = "Ctrl + alt + shift + down is clicked"
      },

      submit() {
        console.log("form is submitted, the value is", this.firstName);
      }
    }
  }

</script>
