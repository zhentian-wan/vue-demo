<template>
    <section class="container">
        <h1 class="title">
            {{message}}
        </h1>
        <button @click="changeMessage" class="button">Change Message</button>
        <hr>
        <section>
            <h2>Mouse event</h2>
            <div>{{counter}}</div>
            <div @mouseover="inc">Mouse over here to change counter</div>
        </section>
        <section>
            <h2>Keyboard events</h2>
            <form @submit.prevent="submit">
                <input type="text"
                       v-model="firstName"
                       @keyup.enter="submit"
                       @keyup.alt.ctrl.shift.down="keyeventHandler"/>
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
  export default {
    data() {
      return {
        message: 'This is my vue!',
        counter: 0,
        key: "",
        firstName: ""
      }
    },

    methods: {
      changeMessage() {
        this.message = "Updated message here!"
      },

      inc() {
        this.counter += 1;
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
