<template>
  <form>
    <label for="email">Email</label>
    <input type="email" v-model="email" />

    <label for="password">Password</label>
    <input type="password" v-model="password" />

    <label for="role">Role</label>
    <select name="role" id="role" v-model="role">
      <option value="ui">UI Designer</option>
      <option value="frontend">Frontend</option>
      <option value="backend">Backend</option>
      <option value="db">DB Admin</option>
    </select>

    <div class="keywords">
      <label>Skills</label>
      <input
        type="checkbox"
        name="html"
        id="html"
        value="html"
        v-model="keywords"
      />
      <label for="html">html</label>
      <input
        type="checkbox"
        name="css"
        id="css"
        value="css"
        v-model="keywords"
      />
      <label for="css">css</label>
      <input
        type="checkbox"
        name="javascript"
        id="javascript"
        value="javascript"
        v-model="keywords"
      />
      <label for="javascript">javascript</label>
      <input
        type="checkbox"
        name="vue"
        id="vue"
        value="vue"
        v-model="keywords"
      />
      <label for="vue">Vue</label>
    </div>
    <label for="otherSkills">Other skills</label>
    <input
      @keypress.enter="handleKeyword"
      v-model="currentOtherKeyword"
      id="otherSkills"
      name="otherSkills"
      type="text"
    />
    <small>Write the skill and press enter to add it</small>
    <h3>Chosen skills:</h3>
    <div class="chosenSkills">
      <div
        @click="keywords.delete(`${skill}`)"
        v-for="skill in keywords"
        :key="skill"
        class="skill-card"
        type="button"
      >
        {{ skill }}
      </div>
    </div>
    <div class="tac">
      <input type="checkbox" name="tac" id="tac" v-model="tac" required />
      <label for="tac">Accept terms and conditions</label>
    </div>
  </form>
</template>

<script>
export default {
  name: "SignUpForm",
  data() {
    return {
      email: "",
      password: "",
      role: "",
      tac: false,
      keywords: new Set(),
      currentOtherKeyword: "",
    };
  },
  methods: {
    handleKeyword() {
      if (this.currentOtherKeyword.trim().length > 0) {
        // To lowercase for getting rid of duplicates
        this.keywords.add(this.currentOtherKeyword.toLowerCase());
        this.currentOtherKeyword = "";
      }
    },
  },
};
</script>

<style>
h3 {
  margin: 0.5em 0;
  color: #aaa;
}
form {
  max-width: 420px;
  margin: 30px auto;
  background-color: #fff;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
.keywords label:first-child {
  display: block;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 5px 0 10px;
  position: relative;
  top: 2px;
}
.chosenSkills {
  display: flex;
  flex-wrap: wrap;
}
.skill-card {
  border: 1px dashed #ddd;
  color: #aaa;
  margin: 0.5em;
  padding: 0.5em;
}
</style>