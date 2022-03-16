<template>
  <div class="main">
    <!-- search filter -->
    <div class="search">
        <input type="text" v-model="searchQuery" placeholder="search">
    </div>
      <table class="table">
        <tbody>
          <tr>
            <th>User ID</th>
            <th>Avatar</th>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Username</th>
            <th>Job Title</th>
            <th>Email</th>
          </tr>

          <tr v-for="user in filterUsers" :key="user.id">
            <td>{{user.id}}</td>
            <td>{{}}</td>
            <td>{{}}</td>
            <td>{{}}</td>
            <td>{{user.username}}</td>
            <td>{{}}</td>
            <td>{{user.email}}</td>
          </tr>
        </tbody>
      </table>

  <!-- --- next and prev pagination -->
      <div class="pagination">
          <button @click="prev">Prev</button>
          <button @click="next">Next</button>
      </div>
  </div>
</template>

<script>
// import axios from 'axios';
// const url = 'http://localhost:3000'
export default {
  name: 'Users',

  data() {
    return {
      users : [
        {
          "id" : 1,
          "email" : "john@gmail.com",
          "username" : "john"
        },
        {
          "id" : 2,
          "email" : "peace@gmail.com",
          "username" : "peace"
        },
        {
          "id" : 3,
          "email" : "anita@gmail.com",
          "username" : "anita"
        },
        {
          "id" : 4,
          "email" : "cindy@gmail.com",
          "username" : "cindy"
        },
        {
          "id" : 5,
          "email" : "david@gmail.com",
          "username" : "david"
        },
        {
          "id" : 6,
          "email" : "zain@gmail.com",
          "username" : "zain"
        },
        {
          "id" : 7,
          "email" : "peter@gmail.com",
          "username" : "peter"
        },
        {
          "id" : 8,
          "email" : "faith@gmail.com",
          "username" : "faith"
        },
        {
          "id" : 9,
          "email" : "giffy@gmail.com",
          "username" : "giffy"
        },
        {
          "id" : 10,
          "email" : "yen@gmail.com",
          "username" : "yen"
        }
      ],
      searchQuery: '',
      currentPage:1,
      pageSize:8,
    }
  },

  mounted() {
    // this.getUsers();
  },

  computed: {
    filterUsers() {
            const query = this.searchQuery.toLowerCase()
            if(this.searchQuery) {
               return this.users.filter((user) => {  
                     return Object.values(user).some((word) => String(word).toLowerCase().includes(query))
                })
            }  else {
                return this.users.filter((row, index) => {
                let start = (this.currentPage -1)*this.pageSize;
                let end = this.currentPage*this.pageSize;
                if(index >= start && index < end) return true;
                })
            }
        }
  },

  methods: {
    // getUsers() {
    //   axios({
    //     method: 'GET',
    //     url: `${url}/db`,
    //     headers: {
    //         'Content-type': 'application/json'
    //     },
    //     })
    //     .then((response)=> {
    //         this.users = response.data
    //         console.log(this.users);
    //     })
    //     .catch((error) => {
    //         console.log(error)
    //     })
    // },

    next() {
      if((this.currentPage*this.pageSize) < this.users.length) this.currentPage++;
    },

    prev() {
      if(this.currentPage > 1) this.currentPage--
    }
  }
  
}
</script>

<style scoped>
.main {
  margin-top: 5rem;
}
.search {
  text-align: center;
  margin-bottom: 2rem;
}
.search input{
  padding: .5rem;
  border-radius: .5rem;
  border: none;
  border: 1px solid grey;
  outline: none;
}
.table {
  width: 50%;
  margin: auto;
}
.table th {
  text-align: left;
  color: royalblue;
}
.pagination {
  text-align: center;
  margin-top: 2rem;
}
.pagination button {
  margin-right: 1rem;
  padding: .2rem;
  border-radius: .3rem;
  outline: none;
  border: none;
  border: 1px solid royalblue;
  background: transparent;
  width: 5rem;
  cursor: pointer;
}
</style>
