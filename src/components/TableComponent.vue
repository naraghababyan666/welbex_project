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
        <tr v-for="item in displayedPosts" :key="item.id">
          <td>{{ item.date }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.count }}</td>
          <td>{{ item.distance }}</td>
        </tr>
      </tbody>

    </table>
    <nav aria-label="Page navigation example" class="navigation">
      <ul class="pagination">
        <li class="page-item">
          <button type="button" class="page-link" v-for="(pageNumber, index) in pages" :key="index" :class="{'active_page' : active_page === pageNumber }" @click="changePage(pageNumber)"> {{pageNumber}} </button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import axios from "axios";
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
      // list: [],
      page: 1,
      count_per_page: 4,
      pages: [],
      active_page: 1,
      isActive: true,
    }
  },
  methods: {
    getLists(){
      axios.post('https://apimocha.com/welbex/lists').then((res) => {
        this.list = res.data.data
        this.setPages(this.list)
      })
    },
    setPages (list) {
      let numberOfPages = Math.ceil(list.length / this.count_per_page);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate () {
      let page = this.page;
      let perPage = this.count_per_page;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      return  this.list.slice(from, to);
    },
    changePage(int){
      this.page = int
      this.active_page = int
    }
  },
  computed: {
    displayedPosts () {
      return this.paginate(this.posts);
    }
  },
  mounted() {
    // this.setPages()
    this.getLists()
  }
}
</script>

<style lang="scss" scoped>
.active_page{
  transform: scale(1.1);
}
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
  .navigation{
    .pagination{
      .page-item{
        list-style-type: none;
        button{
          background: transparent;
          border: 1px solid grey;
          padding: 5px 20px;
          font-size: 20px;
          &:not(:last-child){
            margin-right: 10px;
          }
        }
      }
    }
  }

}
</style>
