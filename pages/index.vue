<template>

    <section class="container">
        <item-description
            v-bind:counter = "counter"
            v-bind:name = "message"
            @total="getTotalFromChild"
        ></item-description>
        <span>Get total: {{total}}</span>
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
        <section>
            <h3>Dynamic component</h3>
            <a @click="toggle">{{toggleButton}}</a>
            <keep-alive>
                <component
                        v-bind:is="currentView"
                        v-bind:name="message"
                >
                </component>
            </keep-alive>

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
  import ShowComponent from '../components/show';
  import EditComponent from '../components/edit';

  export default {
    data() {
      return {
        message: 'this is my vue!',
        counter: 0,
        key: "",
        firstName: "",
        buttonText: "Add",
        total: 0,
        currentView: "ShowComponent"
      }
    },

      computed: {
        buttonDisabled: function() {
          return this.firstName == "";
        },

        toggleButton: function() {
            return this.currentView === "ShowComponent" ?
                'show': 'Edit';
        }
      },
      watch: {
        firstName: function(){
          this.buttonText = this.firstName !== "" ? "Add " + this.firstName : "Add Dinosaur";
        }
      },

    components: {
        ItemDescription,
        EditComponent,
        ShowComponent
    },

    filters: {
        capitalize(value) {
            return value.charAt(0).toUpperCase() + value.slice(1).toLowerCase();
        }
    },

    methods: {
      toggle() {
        this.currentView =
            this.currentView === "ShowComponent" ?
            "EditComponent" : "ShowComponent";
      },
      getTotalFromChild(val) {
         this.total = val;
      },
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
