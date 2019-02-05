<template>
  <v-container>
    <div>
      <h1>{{title}}</h1>
    </div>
    <v-form v-model="valid">
      <v-text-field v-model="name" :rules="nameRules" label="Name" required></v-text-field>
      <v-text-field v-model="description" :rules="descriptionRules" label="Description" required></v-text-field>
      <v-btn @click="submit" :disabled="!valid" color="success">submit</v-btn>
    </v-form>
    <v-card v-for="item in todoItem" :key="item">
      <v-card-title primary-title>
        <div>
          <h2>{{item.name}}</h2>
          <div>{{item.description}}</div>
        </div>
      </v-card-title>
      <v-card-actions>
        <v-btn @click="deleteThis(item.id)" color="error"><i class="material-icons left">delete</i></v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    title: "Todo App",
    nextId: 1,
    todoItem: [{ id: 0, name: "test", description: "test desc" }],
    valid: false,
    name: "",
    description: "",
    nameRules: [v => !!v || "Name is required"],
    descriptionRules: [v => !!v || "Description is required"]
  }),
  methods: {
    submit: function() {
      let name = this.$data.name;
      let description = this.$data.description;
      let id = this.$data.nextId;
      this.$data.nextId++;
      this.$data.todoItem.push({id, name, description });
    },
    deleteThis: function(button_id) {
      let i = 0;
      for(let j = 0; j < this.$data.todoItem.length; j++) {
        if (this.$data.todoItem[j].id == button_id) {
          break;
        } 
        i++
      }
      this.$data.todoItem.splice(i, 1);
    }
  }
};
</script>

<style>
</style>
