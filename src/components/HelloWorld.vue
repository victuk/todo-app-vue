<template>
<ComponentA :name="msg" :name2="msg2"></ComponentA>
</template>

<script>
const ComponentA = {
  template: `<div> Hello {{name}}, i am going to make {{name2}}
  </div>`,
  props: ['name', 'name2'],
};

export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      msg2: 'anoda',
    };
  },
  components: {
    ComponentA,
  },
};
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
