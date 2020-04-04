<template>
  <div id="activity-app">
    <nav class="navbar is-white topNav">
      <div class="container">
        <div class="navbar-brand">
          <h1>Activity Planner</h1>
        </div>
      </div>
    </nav>
    <nav class="navbar is-white">
      <div class="container">
        <div class="navbar-menu">
          <div class="navbar-start">
            <a class="navbar-item is-active" href="#">Newest</a>
            <a class="navbar-item" href="#">In Progress</a>
            <a class="navbar-item" href="#">Finished</a>
          </div>
        </div>
      </div>
    </nav>

    <section class="container">
      <div class="columns">
        <div class="column is-3">
          <a
            v-if="!isFormDisplayed"
            class="button is-primary is-block is-alt is-large"
            
            @click="togglefunction"
          >New Activity</a>
          <div v-if="isFormDisplayed" class="create-form">
            <h2>Create Activity</h2>
            <form>
              <div class="field">
                <label class="label">Title</label>
                <div class="control">
                  <input
                    v-model="viewgoal.title"
                    class="input"
                    type="text"
                    placeholder="Read a Book"
                  />
                </div>
              </div>

              <div class="field">
                <label class="label">Notes</label>
                <div class="control">
                  <textarea
                    v-model="viewgoal.note"
                    class="textarea"
                    placeholder="Write some notes here"
                  />
                </div>
              </div>

              <div class="field is-grouped">
                <div class="control">
                  <button class="button is-link" v-bind:disabled="!disable" @click="newactivity">Create Goal</button>
                </div>
                <div class="control">
                  <button class="button is-link" @click="togglefunction">Cancel</button>
                </div>
              </div>
            </form>
          </div>
        </div>

        <div class="column is-9">
          <div class="box content">
            <activityitem v-for="goal in goals" :key="goal.id" :goal="goal" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import activityitem from "./components/activityitem";
import  {fetchActivity,fetchCategory,fetchUser}  from "@/api"




export default {
  name: "App",
  components: { activityitem },
  data() {
    return {
      isFormDisplayed: false,
      message: "Hello Vue!",
      titleMessage: "Title Message Vue!!!!!",
      isTextDisplayed: true,
      viewgoal: {
        title: "",
        note: ""
      },

      user: {
       
      },
      goals: {},
      categories: {}
    };
  },

  beforeCreate() {
    console.log("before create");
  },
  created() {
    this.goals = fetchActivity();
    this.user= fetchUser();
    this.categories=fetchCategory();

    console.log(this.user)
  },


  computed:{
      disable(){
        return this.viewgoal.title && this.viewgoal.note
      }
  },

  methods: {
    foo: function() {
      this.isTextDisplayed = !this.isTextDisplayed;
    },
    togglefunction: function() {
      this.isFormDisplayed = !this.isFormDisplayed;
    },
    newactivity() {
      console.log(this.viewgoal);
    }
  }

};
</script>

<style>
#activity-app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
html,
body {
  font-family: "Open Sans", serif;
  background: #f2f6fa;
}
footer {
  background-color: #f2f6fa !important;
}
.topNav {
  border-top: 5px solid #3498db;
}
.topNav .container {
  border-bottom: 1px solid #e6eaee;
}
.container .columns {
  margin: 3rem 0;
}
.navbar-menu .navbar-item {
  padding: 0 2rem;
}
aside.menu {
  padding-top: 3rem;
}
aside.menu .menu-list {
  line-height: 1.5;
}
aside.menu .menu-label {
  padding-left: 10px;
  font-weight: 700;
}
.button.is-primary.is-alt {
  background: #00c6ff;
  background: -webkit-linear-gradient(to bottom, #0072ff, #00c6ff);
  background: linear-gradient(to bottom, #0072ff, #00c6ff);
  font-weight: 700;
  font-size: 14px;
  height: 3rem;
  line-height: 2.8;
}
.media-left img {
  border-radius: 50%;
}
.media-content p {
  font-size: 14px;
  line-height: 2.3;
  font-weight: 700;
  color: #8f99a3;
}
article.post {
  margin: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #e6eaee;
}
article.post:last-child {
  padding-bottom: 0;
  border-bottom: none;
}
.menu-list li {
  padding: 5px;
}

.navbar-brand > h1 {
  font-size: 31px;
  padding: 20px;
}
</style>
