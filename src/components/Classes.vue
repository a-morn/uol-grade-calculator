<template>
  <table>
    <thead>
      <tr>
        <th>Level</th>
        <th>Code</th>
        <th>Module name</th>
        <th>Type</th>
        <th colspan="2">Credits (actual | weighted)</th>
        <th>Grade (%)</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="classData in classes" :key="classData.name">
        <td>{{classData.level}}</td>
        <td>{{classData.code}}</td>
        <td>{{classData.name}}</td>
        <td>{{classData.compulsory ? 'Compulsory' : 'Optional'}}</td>
        <td>{{classData.credits}}</td>
        <td>{{weightedCredits(classData.credits, classData.level)}}</td>
        <td><input
              v-bind:class="{ error: !isZeroToHundred(classData.grade) }"
              v-model="classData.grade"
              type=number
              min=0
              max=100></td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td colspan=7>Final grade</td>
      </tr>
      <tr>
        <td colspan=7>{{ finalGrade(classes) }}</td>
      </tr>
    </tfoot>
  </table>
</template>

<script>
import classes from '../data/classes.json'

export default {
  name: 'Classes',
  data() {
    return {
      classes
    }
  },
  methods: {
    weightedCredits(credits, level) {
      switch (level) {
        case 4:
          return credits
        case 5:
          return 3 * credits
        case 6:
          return 5 * credits
        default:
          throw new Error(`unsupported level ${level}`)
      }
    },
    finalGrade(classes) {
      const gradedClasses = classes
        .filter(c => c.grade !== undefined && c.grade !== '')

      let percentage = 0

      if (gradedClasses.length) {
        const totalWeightedCredits = gradedClasses
        .reduce((acc, val) => acc + this.weightedCredits(val.credits, val.level), 0)

        const totalWeightedGrade = gradedClasses
          .reduce((acc, val) => acc + this.weightedCredits(val.credits, val.level) * val.grade, 0)

        percentage = (totalWeightedGrade / totalWeightedCredits).toFixed(2)
      }

      return `${percentage}%`
    },
    isZeroToHundred(input) {
      return input === undefined ||
        input === '' ||
        !isNaN(input) &&
        !isNaN(parseFloat(input)) &&
        parseFloat(input) >= 0 && parseFloat(input) <= 100
    }
  }
}

</script>

<style scoped>
table {
  background: #24494B;
  list-style: none;
  margin: 0;
  padding: 32px;
}

td, th {
  border: 1px solid #517E77;
  padding: 0.5rem;
  text-align: center;
}

input.error {
  background: #D73E27;
}
</style>
