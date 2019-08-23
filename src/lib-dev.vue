<script>
import { WorkbookProvider, SheetProvider } from './entry';

export default {
  name:  'VueSheetProviderLibDev', // vue library dev component
  components: {
    WorkbookProvider,
    SheetProvider
  },
  computed: {
    url () {
      return process.env.VUE_APP_SHEET_URL
    }
  }
}
</script>

<template>
  <div class="vue-sheet-provider-lib-dev">
    <workbook-provider :url="url">
      <template #default="{ sheetkey, workbook }">
        <sheet-provider v-if="workbook" :sheetkey="sheetkey" :sheetid="workbook.sheets[0].id">
          <template #default="{ sheet }">
            <table>
              <tr>
                <th v-for="(header, index) in sheet.headers" :key="index">
                  {{ header }}
                </th>
              </tr>
              <tr v-for="(row, index) in sheet.rows" :key="index">
                <td v-for="(cell, index) in row" :key="index">
                  {{ cell }}
                </td>
              </tr>
            </table>
          </template>
        </sheet-provider>
      </template>
    </workbook-provider>
  </div>
</template>

<style scoped>
table {
  border: 1px solid #ccc;
}

th, td {
  border-bottom: 1px solid #ccc;
  border-right: 1px solid #ccc;
  padding: 1rem;
}

th {
  background-color: #ccc;
  color: #fff;
}
</style>
