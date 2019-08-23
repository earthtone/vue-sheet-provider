<script>
import { urlToKey, getWorkbook } from 'sheetsy'

export default {
  name: 'workbook-provider',
  props: {
    url: {
      type: String,
      required: true
    }
  },
  data () {
    return { workbook: null }
  },
  render () {
    return this.$scopedSlots.default({
      workbook: this.workbook,
      sheetkey: this.sheetkey
    })
  },
  methods: {
    async getWorkBook () {
      try {
        this.workbook = await getWorkbook(this.sheetkey)
      } catch (err) {
        console.error(err)
      }
    }
  },
  created () {
    this.sheetkey = urlToKey(this.url)
    this.getWorkBook()
  }
}
</script>
