<template>
  <q-page>
    <div class="q-pa-md">
    <q-table
      title="Treats"
      :data="data"
      :columns="columns"
      row-key="id"
      :filter="filter"
      :loading="loading"
    >

      <template v-slot:top>
        <span class="text-h5 text-weight-light q-pa-md">
        <span class="text-blue-grey-14">Data Transaksi</span>
      </span>
        <!-- <q-btn class="q-ml-sm" color="primary" :disable="loading" label="Remove row" @click="removeRow" /> -->
        <q-space />
        <q-input borderless dense debounce="300" color="primary" v-model="filter">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>

    </q-table>
  </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      filter: '',
      rowCount: 10,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Kode Transaksi',
          align: 'left',
          field: row => row.kodeTr,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'namaPem', align: 'center', label: 'Nama Pembeli', field: 'namaPem', sortable: true },
        { name: 'judulBuku', align: 'center', label: 'Judul Buku', field: 'judulBuku', sortable: true },
        { name: 'hargaBuku', align: 'center', label: 'Harga Buku', field: 'hargaBuku', sortable: true },
        { name: 'jumbel', label: 'Jumlah Beli', align: 'center', field: 'jumbel' },
        { name: 'total', label: 'Total', align: 'center', field: 'total' }
      ],
      data: [
        {
          kodeTr: 'BR--001',
          namaPem: 'Kim HanBin',
          judulBuku: 'Pemrograman 3',
          hargaBuku: 25000,
          jumbel: 4,
          total: 100000
        },
        {
          kodeTr: 'BR--002',
          namaPem: 'Lalisa Blackpink',
          judulBuku: 'Prak. Pemrograman 3',
          hargaBuku: 35000,
          jumbel: 2,
          total: 70000
        },
        {
          kodeTr: 'BR--003',
          namaPem: 'G-Dragon',
          judulBuku: 'Web Programming',
          hargaBuku: 125000,
          jumbel: 5,
          total: 625000
        },
        {
          kodeTr: 'BR--004',
          namaPem: 'Chanyeol',
          judulBuku: 'Web Programming',
          hargaBuku: 125000,
          jumbel: 1,
          total: 125000
        },
        {
          kodeTr: 'BR--005',
          namaPem: 'Park Seo-jon',
          judulBuku: 'Pemrograman 3',
          hargaBuku: 25000,
          jumbel: 5,
          total: 125000
        }
      ]
    }
  },

  methods: {
    // emulate fetching data from server
    addRow () {
      this.loading = true
      setTimeout(() => {
        const
          index = Math.floor(Math.random() * (this.data.length + 1)),
          row = this.original[Math.floor(Math.random() * this.original.length)]
        if (this.data.length === 0) {
          this.rowCount = 0
        }
        row.id = ++this.rowCount
        const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
        this.data = [...this.data.slice(0, index), addRow, ...this.data.slice(index)]
        this.loading = false
      }, 500)
    },

    removeRow () {
      this.loading = true
      setTimeout(() => {
        const index = Math.floor(Math.random() * this.data.length)
        this.data = [...this.data.slice(0, index), ...this.data.slice(index + 1)]
        this.loading = false
      }, 500)
    }
  }
}
</script>
