<template>
  <v-row class="fill-height">
    <v-col
      class="d-flex justify-center align-center"
      cols="12"
    >
      <v-card width="700">
        <v-card-title>
          My Todo List
        </v-card-title>

        <v-divider></v-divider>

        <v-card-text>

          <v-list>
            <v-list-item
              v-for="(item, index) in items"
              :key="item.id"
            >
              <v-list-item-content>
                <v-list-item-title>{{ item.id }}. {{ item.title }}</v-list-item-title>
                <v-list-item-subtitle>
                  {{ item.description }}
                </v-list-item-subtitle>
              </v-list-item-content>

              <v-list-item-action>
                <div
                  class="d-flex"
                >
                  <v-checkbox
                    :input-value="item.isCompleted"
                    v-model="item.isCompleted"
                  ></v-checkbox>
                  <v-icon
                    class="mx-2"
                    @click="populateItem(index)"
                  >mdi-pencil</v-icon>
                  <v-icon
                    @click="deleteItem(index)"
                  >mdi-delete</v-icon>
                </div>
              </v-list-item-action>
            </v-list-item>
          </v-list>

        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions class="d-block">
          <v-text-field
            v-model="title"
            label="Title"
            class="mx-1"
          ></v-text-field>
          <v-text-field
            v-model="description"
            label="Description"
            class="mx-1"
          ></v-text-field>
          <v-btn
            color="primary"
            class="mx-1"
            @click="saveItem"
          >
            Save
          </v-btn>
        </v-card-actions>

      </v-card>
    </v-col>

    <v-col
      cols="6"
      class="px-12"
    >
      <h1> Completed Tasks </h1>
      <ul>
        <li
          v-for="item in completedItems"
          :key="item.id"
        >
          {{ item.title }}
        </li>
      </ul>
    </v-col>

    <v-col
      cols="6"
      class="px-12"
    >
      <h1> Remaining Tasks </h1>
      <ul>
        <li
          v-for="item in remainingItems"
          :key="item.id"
        >
          {{ item.title }}
        </li>
      </ul>
    </v-col>

  </v-row>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          id: 1,
          title: 'Eat Food',
          description: 'Eat Grilled Chicken with Spicy Sauce',
          isCompleted: true,
        },
        {
          id: 2,
          title: 'Sleep Well',
          description: 'Sleep at 12 AM and wake up at 11 AM',
          isCompleted: false,
        },
      ],
      title: '',
      description: '',
      indexToEdit: '',
    };
  },
  computed: {
    completedItems() {
      return this.items.filter((item) => item.isCompleted);
    },
    remainingItems() {
      return this.items.filter((item) => !item.isCompleted);
    },
  },
  methods: {
    saveItem() {
      if (this.indexToEdit !== '') {
        this.editItem();
      } else {
        this.addItem();
      }

      this.title = '';
      this.description = '';
    },
    addItem() {
      const newItem = {
        id: this.items.length + 1,
        title: this.title,
        description: this.description,
        isCompleted: false,
      };
      this.items.push(newItem);
    },
    editItem() {
      const updatedItem = {
        id: this.items[this.indexToEdit].id,
        title: this.title,
        description: this.description,
        isCompleted: this.items[this.indexToEdit].isCompleted,
      };

      this.$set(this.items, this.indexToEdit, updatedItem);

      // INFO: Alternative approach to update array.
      // const duplicateArray = [...this.items];
      // duplicateArray[this.indexToEdit] = updatedItem;
      // this.items = [...duplicateArray];

      this.indexToEdit = '';
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
    populateItem(index) {
      this.indexToEdit = index;
      this.title = this.items[index].title;
      this.description = this.items[index].description;
    },
  },
};
</script>
