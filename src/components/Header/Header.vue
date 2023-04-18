<script setup>
import { ref } from "vue";
const header = ref("Shoping List App");
const editing = ref(false);
const items = ref([
  { id: 1, label: "10 party hats", purchased: true },
  { id: 2, label: "2 board games", purchased: true },
  { id: 3, label: "20 cups", purchased: false },
]);
const newItem = ref("");
const newItemPriority = ref(false);
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value });
};

const doEdit = (evt) => {
  editing.value = evt;
  newItem.value = "";
};

const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
</script>
<template>
  <div class="wrapper">
    <div class="header">
      <h2>{{ header }}</h2>
      <button
        class="btn"
        disabled="newItem.length < 5"
        v-if="editing"
        @click="doEdit(false)"
      >
        Cancel
      </button>
      <button class="btn btn-primary" v-else @click="doEdit(true)">
        Add item
      </button>
    </div>
    <form
      class="wrapper w-50"
      @submit.prevent="saveItem"
      newItem.value=""
      v-if="editing"
    >
      <input
        class="form-control"
        type="text"
        v-model.trim="newItem"
        placeholder="add item shoping"
      />
      Priority:
      <label class="checkboxItem">
        <input type="checkbox" v-model="newItemPriority"/>
        High Priority
      </label>
      <button class="btn btn-primary w-50 save__btn">Save Add</button>
    </form>
    <ul class="shoping__list">
      <li
      v-for="({ id, label, purchased}, index) in items"
      :key="id"
      class="tatic-class"
      :class="{strikeout: purchased}"
      @click="togglePurchased(items[index])"
      >
        {{ label }}
      </li>
    </ul>
    <p class="text-danger" v-if="!items.length">Nothing to see here</p>
  </div>
</template>

<style>
body {
  background-color: #ECF6FFFF;
}
.wrapper {
  display: flex;
  flex-direction: column;
  width: 600px;
  font-size: 24px;
  font-weight: bold;
  color: #323641ff;
  background-color: #fff;
  text-align: center;
  margin: 0 auto;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 20px;
}

.shoping__list {
  list-style-type: none;
}

.checkboxItem {
  font-size: 17px;
}

.save__btn {
  margin: 0 auto;
}

.strikeout {
  color: #B8BEC3FF;
  cursor: pointer;
  font-size: 18px;
  text-decoration: line-through;
}

.tatic-class {
  cursor: pointer;
}
</style>