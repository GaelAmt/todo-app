<template>
  <v-container>
    <v-flex xs6 offset-sm3>
      <div>
        <h1>{{title}}</h1>
      </div>
    </v-flex>
    <v-flex xs6 offset-sm3>
      <v-form v-model="valid">
        <v-text-field v-model="name" :rules="nameRules" label="Name" required></v-text-field>
        <v-text-field v-model="description" :rules="descriptionRules" label="Description" required></v-text-field>
        <v-btn @click="addTodo" :disabled="!valid" color="success"><i class="material-icons left">add</i></v-btn>
      </v-form>
    </v-flex>
    <v-flex xs6 offset-sm3>
      <v-card v-for="(item, index) in todoItem" :key="index">
        <v-card-title primary-title>
          <div>
            <h2>{{item.name}}</h2>
            <div>{{item.description}}</div>
          </div>
        </v-card-title>
        <v-card-actions>
          <v-btn @click="deleteThis(index)" color="error">
            <i class="material-icons left">delete</i>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    title: "Todo App",
    todoItem: [],
    valid: false,
    name: "",
    description: "",
    nameRules: [v => !!v || "Name is required"],
    descriptionRules: [v => !!v || "Description is required"]
  }),
  methods: {
    addTodo: function() {
      let name = this.name;
      let description = this.description;
      this.todoItem.push({ name, description });
    },
    deleteThis: function(index) {
      this.todoItem.splice(index, 1);
    }
  }
};
</script>

<style>
</style>
