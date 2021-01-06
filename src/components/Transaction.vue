<template>
  <h2>Transaction # {{ data.id }}</h2>
  <table v-if="data.id">
    <thead>
      <tr>
        <th>key</th>
        <th>value</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in Object.entries(data)" :key="item">
        <td>{{ item[0] }}</td>
        <td>{{ item[1] }}</td>
      </tr>
      <tr>
        <td>Tags</td>
        <td>
          <tr>
            <th>name</th>
            <th>value</th>
          </tr>
          <tr v-for="tag in tags" :key="tag">
            <td>{{ tag.name }}</td>
            <td>{{ tag.value }}</td>
          </tr>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "Transaction",
  props: {
    data: Object,
    tags: Object
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
