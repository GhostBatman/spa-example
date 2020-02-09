<template>
  <tr v-if="editMode">
    <td>
      <div class="input-group input-group-sm">
        <input type="text"
               class="form-control"
               placeholder="Имя"
               v-model="mutableUser.name" />
      </div>

    </td>
    <td>
      <div class="input-group input-group-sm">
        <input type="text"
               class="form-control"
               placeholder="Телефон"
               v-model="mutableUser.tel" />
      </div>
    </td>
    <td>
      <div class="btn-group btn-group-sm" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-primary" @click="save()">Сохранить</button>
        <button type="button" class="btn btn-secondary" @click="cancel()">Отмена</button>
      </div>
    </td>
  </tr>

  <tr v-else>
    <td>{{user.name}}</td>
    <td>{{user.tel}}</td>
    <td>
      <div class="btn-group btn-group-sm" role="group" aria-label="Basic example">
        <button
          class="btn btn-primary"
          @click="editModeChange()">
          Edit
        </button>
        <button
          class="btn btn-danger"
          @click="removeEvent()">
          Delete
        </button>
      </div>
    </td>
  </tr>
</template>

<script>
/* eslint-disable indent */
export default {
  name: 'UserComponent',
  props: {
    user: {
      type: Object
    }
  },
  data() {
    return {
      editMode: false,
      mutableUser: {
        name: '',
        tel: ''
      }
    }
  },
  methods: {
    editModeChange() {
      this.editMode = !this.editMode
      if(this.editMode) {
        this.mutableUser = Object.assign({}, this.user);
      }
    },
    cancel() {
      this.editModeChange()
    },
    save() {
      this.editModeChange()
      this.$emit('update', Object.assign({}, this.mutableUser))

    },
    removeEvent() {
      this.$emit('remove', this.user)
    }
  }
}
</script>