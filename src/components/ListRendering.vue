<template>
  <div>
    <table>
      <thead>
        <tr>
          <th @click="fieldToSort = 'id'">Id</th>
          <th @click="fieldToSort = 'name'">Name</th>
          <th @click="fieldToSort = 'grade'">Grade</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in listItems" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.grade }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';

@Component
export default class ListRendering extends Vue {
  @Prop()
  private list!: any[];
  private fieldToSort = 'id';

  private get listItems() {
    return this.list.slice().sort((a, b) => {
      return a[this.fieldToSort].toString().localeCompare(b[this.fieldToSort].toString());
    });
  }
}
</script>

<style lang="scss" scoped>
  table {
    border: 1px solid grey;

    th {
      font-weight: bold;
      cursor: pointer;
    }

    th, td {
      border: 1px solid grey;
      padding: 8px;
    }
  }
</style>