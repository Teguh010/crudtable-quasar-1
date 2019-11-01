<template>
  <div class="q-pa-md">
   <q-table
        title="Treats"
        :data="siswa"
        :columns="columns"
        row-key="id"
      >
       <template v-slot:top>
         <q-btn label="Tambah" color="primary" @click="addSiswa" />
      </template> 
        <template v-slot:body-cell-actions="props">
          <q-td :props="props">
            <q-btn dense round flat color="grey" @click="editRow(props)" icon="edit"></q-btn>
            <q-btn dense round flat color="grey" @click="deleteRow(props)" icon="delete"></q-btn>
          </q-td>          
        </template>     
    </q-table>
      <q-dialog v-model="showDialog" persistent>
      <q-card style="width: 350px">
        <q-bar>
          <q-icon name="save" />
          <div>Kelola Data Siswa</div>

          <q-space />

          <q-btn dense flat icon="close" @click="showDialog = !showDialog">

            <q-tooltip>Tutup</q-tooltip>
          </q-btn>
        </q-bar>

        <q-card-section>
          <q-input outlined ref="name" v-model="form.name" label="name" placeholder="name lengkap siswa"
            :rules="[val => !!val || 'name Lengkap Harus disisi']"
             />
        </q-card-section>

        <q-card-section>
          <q-input outlined ref="nis" v-model="form.nis" label="NIS" type="number" placeholder="Nomor induk siswa" hint="" 
          :rules="[val => !!val || 'Nis Harus diisi']"
            />
        </q-card-section>

        <q-card-section>
          <q-input outline ref="alamat" v-model="form.alamat" label="alamat" placeholder="alamat siswa"
           :rules="[val => !!val || 'Alamat harus diisi']"
           />
        </q-card-section>

        <q-card-section>
          <q-btn push color="primary" label="SIMPAN" class="full-width" size="lg" 
          @click="simpan"
             />
        </q-card-section>
      </q-card>
    </q-dialog>

    
  </div>
</template>

<script>
import { uid } from 'quasar'
export default {
   data () {
    return {
      showDialog: false,
      form: {
        name: '',
        nis: '',
        alamat: ''
      },
      siswa: [],
      columns: [
        { name: 'name', label: 'Name', align: 'left', field: row => row.name, format: val => `${val}`, sortable: true},
        { name: 'actions', label: 'Actions', field: '', align:'center' },
        { name: 'nis', align: 'center', label: 'NIS', field: 'nis', sortable: true },
        { name: 'alamat', label: 'Alamat', field: 'alamat', sortable: true }
      ],
      siswa: [
        { id: uid(), name: 'Teguh', nis: 123, alamat: 'disini'},
        {id: uid(), name: 'Sumade', nis: 234, alamat: 'sukamanah'},
        {id: uid(), name: 'Parwito', nis: 789, alamat: 'jogja'
        }
      ],
    }
  },
  methods: {
      simpan() {
      const nameSelector = this.$refs.name
      const nisSelector = this.$refs.nis
      const alamatSelector = this.$refs.alamat

       nameSelector.validate()
       nisSelector.validate()
       alamatSelector.validate()

        if (namaSelector.hasError || nisSelector.hasError || emailSelector.hasError || jurusanSelector.hasError || alamatSelector.hasError) console.log("Gagal simpan data siswa")
      else {
        this.addSiswa()
        this.clearForm()
      }
    },
      clearForm() {
        this.form.name = ''
        this.form.nis = ''
        this.form.alamat = ''
        this.showDialog = false
      },

      // showForm(id='') {
      // this.showDialog = true
      // },

      addSiswa() {
        this.siswa.push({
          id: uid(),
          name: this.form.name,
          nis: this.form.nis,
          alamat: this.form.alamat,
        })
      },


    editRow(props) {
      // do something
      this.$q.notify({
        color: 'primary',
        message: `disini untuk edit data => ${JSON.stringify(props.row)}`,
        timeout: 500
      })
    },
    deleteRow(props){
      // do something
      this.$q.notify({
        color: 'negative',
        message: `disini untuk delete data => ${JSON.stringify(props.row)}`,
        timeout: 500
      })
    },
     addRow(props) {
      // do something
      this.$q.notify({
        color: 'primary',
        message: `I'll add row data => ${JSON.stringify(props.row)}`,
        timeout: 500
      })
    },
  }
}
</script>
