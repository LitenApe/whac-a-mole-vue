<template>
  <h2>Highscore!</h2>
  <table>
    <thead>
      <tr>
        <th>#</th>
        <th>Date</th>
        <th>Score</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(datapoint, index) in scores" :key="index">
        <td>{{ index + 1 }}</td>
        <td>{{ datapoint.date }}</td>
        <td>{{ datapoint.score }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'Highscore',
  props: ['scores'],
};
</script>
