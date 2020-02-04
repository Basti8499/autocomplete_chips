<template>
  <div id="app">
    <v-app>
      <v-container fluid>
        <v-layout wrap align-center column>
          <v-autocomplete
            :value="value"
            :label="label"
            :items="items"
            chips
            box
            multiple
            item-text="title"
            item-value="id"
            @click.stop="open = true;"
          >
            <template slot="selection" slot-scope="data">
              <v-chip
                :selected="data.selected"
                close
                class="chip--select-multi"
                @input="handleClick(data.item);"
              >
                {{ data.item.title }}
              </v-chip>
            </template>
          </v-autocomplete>
        </v-layout>
      </v-container>
    </v-app>
  </div>
</template>

<script>
import posts from "./posts.json";

export default {
  name: "App",
  data: () => ({
    items: posts,
    value: [1, 2, 3, 4, 5, 6, 7, 8, 9],
    label: "label"
  }),
  computed: {
    selected: {
      get() {
        return this.value;
      },
      set(id) {
        const res = this.value;
        if (!res.includes(id)) {
          res.push(id);
        } else {
          const index = res.indexOf(id);
          if (index !== -1) {
            res.splice(index, 1);
          }
        }

        this.$emit("input", res);
      }
    }
  },
  methods: {
    handleClick(value) {
      this.selected = value.id;
    }
  }
};
</script>

<style scoped>
.scroller {
  height: 100%;
}
</style>
