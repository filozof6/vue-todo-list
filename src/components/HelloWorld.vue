<template>
  <div class="hello">
    <div class='jumbotron'>
      <img src='../assets/profile.jpg' class="rounded-circle" ><br>
      <h1>Fullstack Developer</h1>
      <ul>
        <li>
          <a href="https://www.facebook.com/roland.zahradnik" target="_blank">
            <img src="../assets/fb.png" alt="FB icon">
          </a>
        </li>
        <li>
          <a href="https://www.linkedin.com/in/romanzahradnik/" target="_blank">
            <img src="../assets/linkedin.png" alt="LinkedIn icon">
          </a>
        </li>
        <li>
          <a href="https://github.com/filozof6" target="_blank">
            <img src="../assets/git.png" alt="GitHub icon">
          </a>
        </li>
        <li>
          <a href="mailto:rzfilozof@gmail.com" target="_blank">
            <img src="../assets/gmail.png" alt="Gmail icon">
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

</style>
