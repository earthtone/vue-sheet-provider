<script>
import sheetsy from 'sheetsy'

const {
  getSheet
} = sheetsy

export default {
  name: 'sheet-provider',
  props: {
    sheetkey: {
      type: String,
      required: true
    },
    sheetid: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      sheet: null
    }
  },
  render () {
    return this.$scopedSlots.default({
      sheet: this.sheet,
    })
  },
  methods: {
    async getSheet () {
      try {
        this.sheet = await getSheet(this.sheetkey, this.sheetid)
        this.sheet.headers = Object.keys(this.sheet.rows[0]).splice(this.sheet.rows[0].length)
      } catch (err) {
        console.error(err)
      }
    }
  },
  mounted () {
    this.getSheet()
  }
}
</script>
