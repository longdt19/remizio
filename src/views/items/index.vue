<template>
  <div class="animated fadeIn">
    <b-card :header="caption">
      <b-table :hover="hover" :striped="striped" :bordered="bordered" :small="small" :fixed="fixed" responsive="sm" :items="items" :fields="fields" :current-page="currentPage" :per-page="perPage">
        <template slot="action" slot-scope="data">
          <b-button size="sm" v-b-modal.modal @click="load_modal(data)">Edit</b-button>
        </template>
      </b-table>
      <nav>
        <b-pagination :total-rows="getRowCount(items)" :per-page="perPage" v-model="currentPage" prev-text="Prev" next-text="Next" hide-goto-end-buttons/>
      </nav>
    </b-card>
    <b-modal id="modal" title="Edit">
      <b-row class="my-1">
        <b-col sm="3"><label for="input-default">Code:</label></b-col>
        <b-col sm="5">
          <b-form-input id="input-default" size="sm" type="text" placeholder="Enter your name" v-model="modalInfo.code"></b-form-input>
        </b-col>
      </b-row>

      <b-row class="my-1">
        <b-col sm="3"><label for="input-default">Name:</label></b-col>
        <b-col sm="5">
          <b-form-input id="input-default" size="sm" type="text" placeholder="Enter your name" v-model="modalInfo.name"></b-form-input>
        </b-col>
      </b-row>

      <b-row class="my-1">
        <b-col sm="3"><label for="input-default">Category:</label></b-col>
        <b-col sm="5">
          <b-form-input id="input-default" size="sm" type="text" placeholder="Enter your name" v-model="modalInfo.category"></b-form-input>
        </b-col>
      </b-row>
    </b-modal>
  </div>
</template>

<script>
/**
   * Randomize array element order in-place.
   * Using Durstenfeld shuffle algorithm.
   */
const shuffleArray = (array) => {
  for (let i = array.length - 1; i > 0; i--) {
    let j = Math.floor(Math.random() * (i + 1))
    let temp = array[i]
    array[i] = array[j]
    array[j] = temp
  }
  return array
}

export default {
  name: 'c-table',
  props: {
    caption: {
      type: String,
      default: 'Table'
    },
    hover: {
      type: Boolean,
      default: false
    },
    striped: {
      type: Boolean,
      default: false
    },
    bordered: {
      type: Boolean,
      default: false
    },
    small: {
      type: Boolean,
      default: false
    },
    fixed: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    return {
      items: shuffleArray([
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'},
        {code: 123, name: 'Đặng tùng long', category: 'vest', created: '2012/01/01'}
      ]),
      fields: [
        {key: 'code', 'class': 'text-center'},
        {key: 'name', 'class': 'text-center'},
        {key: 'category', 'class': 'text-center'},
        {key: 'created', 'class': 'text-center'},
        {key: 'action', 'class': 'text-center'}
      ],
      currentPage: 1,
      perPage: 5,
      totalRows: 0,
      modalInfo: {}
    }
  },
  methods: {
    load_modal (row) {
      console.log('row', row)
      this.modalInfo = {
        name: row.item.name,
        created: row.item.created,
        category: row.item.category,
        code: row.item.code
      }
    },
    getBadge (action) {
      return action === 'Active' ? 'success'
        : action === 'Inactive' ? 'secondary'
          : action === 'Pending' ? 'warning'
            : action === 'Banned' ? 'danger' : 'primary'
    },
    getRowCount (items) {
      return items.length
    }
  }
}
</script>

<style lang="css">
</style>
