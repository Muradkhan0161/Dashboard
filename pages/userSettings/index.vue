<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    sort-by="email"
    class="elevation-1"
    :search="search"
  >
    <template v-slot:top>
      <v-toolbar flat >
        <v-toolbar-title>User</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
      <v-spacer />
        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ on }">
            <v-btn color="primary" dark class="mb-2" v-on="on">Add new user</v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.name" label="User name"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.email" label="Email"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="editedItem.password" label="Password"></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="save">Save</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn color="primary" @click="initialize">Reset</v-btn>
    </template>
  </v-data-table>
</template>

<script>
  export default {
    data: () => ({
      search: '',
      dialog: false,
      headers: [
        {
          text: 'User Name',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'Email', value: 'email' },
        { text: 'Password', value: 'password', sortable: false },
        { text: 'Total sells', value: 'total' },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        name: '',
        email: '.com',
        password:'',      
      },
      defaultItem: {
        name: '',
        email: '.com',
        password:'',
        total: 0,
      },
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New User' : 'Edit user'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.desserts = [
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 6.0,
            total: 24,
        
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 9.0,
            total: 37,
            
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 16.0,
            total: 23,
           
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 3.7,
            total: 67,
            
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 16.0,
            total: 49,
           
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 0.0,
            total: 94,
           
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 0.2,
            total: 98,
           
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 3.2,
            total: 87,
          
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 25.0,
            total: 51,
        
          },
          {
            name: 'Murad',
            email: 'muradkhan0161@gmail.com',
            password: 26.0,
            total: 65,
         
          },
        ]
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        const index = this.desserts.indexOf(item)
        confirm('Are you sure you want to delete this item?') && this.desserts.splice(index, 1)
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>