<template>
  <div class="container">

    <table >
      <thead>
        <tr>
          <th>Дата</th>
          <th>Название</th>
          <th>Количество</th>
          <th>Расстояние</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in list" :key="item.id">
          <td>{{ item.date }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.count }}</td>
          <td>{{ item.distance }}</td>
        </tr>
      </tbody>

    </table>
    <nav aria-label="Page navigation example">
      <ul class="pagination">
        <li class="page-item">
          <button type="button" class="page-link" v-if="page !== 1" @click="page--"> Previous </button>
        </li>
        <li class="page-item">
          <button type="button" class="page-link" v-for="(pageNumber, index) in pages.slice(page-1, page+5)" :key="index" @click="page = pageNumber"> {{pageNumber}} </button>
        </li>
        <li class="page-item">
          <button type="button" @click="page++" v-if="page < pages.length" class="page-link"> Next </button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: "TableComponent",
  data(){
    return {
      list: [
        {
          'id': 1,
          'date' : '27.09.2022',
          'name' : 'Vie tour',
          'count' : '21',
          'distance' : '150',
        },
        {
          'id': 2,
          'date' : '28.09.2022',
          'name' : 'Line tour',
          'count' : '21',
          'distance' : '150',
        },
        {
          'id': 3,
          'date' : '29.09.2022',
          'name' : 'Counter tour',
          'count' : '21',
          'distance' : '150',
        },
        {
          'id': 4,
          'date' : '15.09.2022',
          'name' : 'Nice tour',
          'count' : '21',
          'distance' : '150',
        },
        {
          'id': 5,
          'date' : '13.09.2022',
          'name' : 'Happy tour',
          'count' : '21',
          'distance' : '150',
        },
        {
          'id': 6,
          'date' : '12.09.2022',
          'name' : 'Boston tour',
          'count' : '21',
          'distance' : '150',
        },
      ],
      page: 1,
      count_per_page: 2,
      pages: []
    }
  },
  methods: {
    setPages () {
      let numberOfPages = Math.ceil(this.list.length / this.count_per_page);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
  },
  mounted() {
    this.setPages()
  }
}
</script>

<style lang="scss" scoped>
.container{
  table {
    border-radius: 10px;
    font-family: Arial, Helvetica, sans-serif;
    border-collapse: collapse;
    width: 100%;
    max-width: 70%;
    margin: 0 auto;
    td, th{
      border: 1px solid #ddd;
      padding: 8px;
      cursor: pointer;
    }
    thead tr{
      padding-top: 12px;
      padding-bottom: 12px;
      text-align: left;
      background-color: #000e96;
      color: white;
    }
    tbody{
      tr:nth-child(even) {
        background-color: #f2f2f2;
        &:hover{
          background-color: #ddd;

        }
      }
    }
  }

}
</style>