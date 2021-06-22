<template>
  <v-row justify="center">
    <!-- persident(v-dialog içine) öğenin dışına tıklayınca pencereyi kapatmaması için -->
    <v-dialog max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn text v-on="on" v-bind="attrs" class="success"
          >Add new project</v-btn
        >
      </template>
      <v-card>
        <v-card-title>
          <h2>Add a New Project</h2>
        </v-card-title>
        <v-card-text>
          <v-container >
            <v-form class="px-3" ref="form">
            <v-row>
              <v-col>
                <v-text-field
                  label="Title"
                  v-model="title"
                  prepend-icon="folder"
                  :rules="inputRules"
                ></v-text-field>
                <v-textarea
                  label="Informantion"
                  v-model="content"
                  prepend-icon="edit"
                ></v-textarea>

                <v-menu>
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      label="Due Date"
                      prepend-icon="date_range"
                      v-on="on"
                      v-bind="attrs"
                      :value="due"
                    ></v-text-field>
                  </template>
                  <v-date-picker v-model="due"></v-date-picker>
                </v-menu>

                <v-btn text class="success mx-0 mt-3" @click="submit"
                  >Add project</v-btn
                >
              </v-col>
            </v-row>
            </v-form>
          </v-container>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
import format from 'date-fns/format'
export default {
  data() {
    return {
      title: "",
      content: "",
      due: null,
      inputRules: [
        v => v.length >= 3 || 'Minimum length is 3 characters'
      ]
    };
  },
  methods: {
    submit() {
      if(this.$refs.form.validate()) {
        console.log(this.title, this.content)
      }
    },
  },
  computed: {
    formattedDate(){
      return this.due ? format(this.due,'DD MM YYYY') : ''
    }
  }
};
</script>
