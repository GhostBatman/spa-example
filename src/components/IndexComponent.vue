<template>
  <div class="row justify-content-center">
    <div class="col-md-8">
      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th>Имя</th>
            <th>Тел</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <user-component
            v-for="(user, index) in users"
            :key="user.name"
            :user="user"
            @update="updateUser($event, index)"
            @remove="removeUser($event, index)"
          >
          </user-component>
        </tbody>
      </table>
      <div class="form-row">
        <div class="col-5">
          <input type="text"
                 class="form-control mb-3"
                 placeholder="Имя"
                 v-model="newUser.name" />
        </div>
        <div class="col-5">
          <input type="text"
                 class="form-control mb-3"
                 placeholder="Тел"
                 v-model="newUser.tel" />
        </div>
        <div class="col-2">
          <button class="btn btn-primary mb-3"
                  @click="addNewUser(newUser)">
            Добавить
          </button>
        </div>
      </div>
    </div>
    <div class="col-md-8">
      <div v-if="error" class="alert alert-danger" role="alert">
        {{ error }}
      </div>
    </div>
  </div>

</template>

<script>
import data from '../data'
import UserComponent from './UserComponent'
// import Axios from 'axios'

export default {
  components: { UserComponent },
  name: 'IndexComponent',
  data() {
    return {
      error: '',
      users: [],
      newUser: {
        name: '',
        tel: ''
      }
    }
  },
  created() {
    this.getUsers()
      .then(resp => {
        this.users = resp.data
      })
  },
  methods: {
    getUsers() {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(data)
        }, 1000)
      })
    },
    isValid({ tel, name }) {
      let isValidTel = /^((\+|)+([0-9]){10,15})$/gm.test(tel)
      if (!name.length) {
        this.error = 'Поле имя не может быть пустым'
        return false
      }
      if (!isValidTel) {
        this.error = 'Неверный формат номера телефона'
        return false
      }

      this.error = ''
      return true
    },
    addNewUser(newUser) {
      if (this.isValid(newUser)) {
        this.users.push(newUser)
        // отправка данных на сервер
        // Axios.post('/user/create', newUser, { headers: headers })
        //   .then((resp) => {})
        //   .catch((error) => {})

        this.newUser = {
          name: '',
          tel: ''
        }
      }
    },
    removeUser(user, index) {
      this.users.splice(index, 1)
    },
    updateUser(user, index) {

      if (this.isValid(user)) {
        this.users[index] = user
        this.users = [...this.users]

        // отправка данных на сервер
        // Axios.patch('/user/update', user, { headers: headers })
        //   .then((resp) => {})
        //   .catch((error) => {})
      }
    }
  }
}
</script>