<template>
  <div class="hello">
    <p>{{count}}</p>
    <p>{{object}}</p>
  </div>
</template>

<script lang="ts">
import { ref, reactive } from "vue";

export default {
  setup() {
    const count = ref(0);
    const object = reactive({ foo: "bar" });
    
    // expose to template
    return {
      count,
      object
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
