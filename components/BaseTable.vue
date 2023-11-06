<template>
  <div class="va-table-responsive base-table">
    <table class="base-table va-table va-table--striped">
      <thead class="thead">
        <tr>
          <th
            v-for="(item, i) in tableHeaders"
            :id="i"
            :key="'thead' + i"
            class="th"
            :class="i == 0 && 'p-40'"
            cols="2"
            :width="item.width ? `${item.width}px` : 'fit-content'"
            :min-width="item.minWidth"
          >
            <span class="header-title">{{ item.label }}</span>
          </th>
          <th>
            <span>Action</span>
          </th>
        </tr>
      </thead>
      <tbody class="tbody">
        <tr v-for="(n, i) in tableItems" :key="'tbody-tr' + i" class="tr">
          <td
            v-for="(k, j) in tableHeaders"
            :key="'tbody-tr-td' + j"
            class="td"
            :width="n.width ? `${n.width}px` : 'fit-content'"
            :min-width="n.minWidth"
          >
            {{ n[k.value] }}
          </td>
          <td class="table-action" :class="i % 2 !== 0 ? 'custom' : ''">
            <div class="action-table">
              <button @click="handleEdit(i)">
                <va-icon class="mr-2 edit-icon" name="edit" color="#000000" />
              </button>
              <button @click="handleDelete(i)">
                <va-icon
                  class="mr-2 delete-icon"
                  name="delete"
                  color="#000000"
                />
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script setup>
defineProps({
  tableHeaders: {
    type: Array,
    default: () => [],
  },
  tableItems: {
    type: Array,
    default: () => [],
  },
});
const emits = defineEmits(["editItem", "deleteItem"]);
const handleEdit = (index) => {
  emits("editItem", index);
};
const handleDelete = (index) => {
  emits("deleteItem", index);
};
</script>
<style scoped lang="scss">
@import url("../assets/scss/common/components/base-table.scss");
</style>
